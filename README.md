# Substack Agentic Editorial Workflow ✍️🤖

Un repository modulare e pronto all'uso per trasformare qualsiasi assistente AI a riga di comando (**Antigravity CLI**, Claude Code, Hermes, Cursor) in una **redazione editoriale aumentata** per la tua pubblicazione Substack.

Basato sul pattern **Agent-Native Workspace (File-as-State)**: nessuna pipeline rigida in script monolitici, ma una collaborazione continua tra autore e intelligenza artificiale direttamente all'interno della sessione di lavoro.

---

## 🏛️ Filosofia: Human-Centric Editorial Board

1. **Zero Ghostwriting:** L'AI non genera mai articoli da zero né si sostituisce alla voce autentica dell'autore.
2. **Critique & Support First:** Gli agenti agiscono come compagni di redazione: ricercatori di trend, sparring partner logici, revisori di refusi, packaging strategist, visual designer ed esecutori tecnici.
3. **Direzione Artistica Coerente:** La creazione visiva non è un'aggiunta casuale o generica: è curata dall'**Art Director** sulla base di una guida di stile visivo (`visual_style.md`), vietando rigorosamente cliché banali, scritte deformate e stili incoerenti.
4. **Human-in-the-Loop Obbligatorio:** L'autore scrive la scaletta (`01_outline.md`) e la prima bozza completa (`03_draft.md`). L'agente interviene per stimolare la riflessione, validare la tenuta logica, correggere i cliché, confezionare titoli e copertina e preparare la pubblicazione.
5. **Deploy Solo Bozza (Draft Only):** Nessun invio automatico a sorpresa. Il workflow si conclude sempre con il caricamento di una **bozza privata (draft)** su Substack, fornendo il link diretto per la preview finale prima dell'invio manuale agli iscritti.

---

## 👥 I Ruoli della Redazione Aumentata

La redazione è composta da sub-agenti specializzati con responsabilità precise:

| Ruolo | Modulo Agente | Responsabilità Principale |
| :--- | :--- | :--- |
| **Bootstrap Profiler** | `agents/00_bootstrap_profiler.md` | Analizza l'archivio storico Substack ed estrae la guida stilistica (`style_guide.md`) e l'identità visiva (`visual_style.md`). |
| **Topic Scout** | `agents/01_topic_scout.md` | Monitora trend, paper e notizie web evitando argomenti già trattati; propone 3 pitch con "Why Now" e bozza di scaletta. |
| **Sparring Partner** | `agents/02_sparring_partner.md` | Dialoga criticamente con l'autore sull'outline, sollevando salti logici e le obiezioni del lettore scettico (senza mai riscrivere la scaletta). |
| **Copy Editor** | `agents/03_copy_editor.md` | Analizza la prima bozza, individua refusi, sintassi involuta e cliché AI vietati, producendo una tabella diff (`04_review_diff.md`). |
| **Packaging Specialist** | `agents/04_packaging_agent.md` | Ottimizza l'open-rate formulando 5 varianti di Subject Line, 2 Preview Text (<90 caratteri) e la CTA finale in `metadata.json`. |
| **Art Director & Visual Designer** | `agents/05_art_director.md` | Estrae la metafora concettuale dell'articolo, applica la palette e le direttive di `visual_style.md`, progetta il prompt in inglese e genera la copertina 16:9 (`assets/cover.png`) via Nano Banana MCP. |
| **Substack Publisher** | `agents/06_substack_publisher.md` | Sanitizza il Markdown, richiede conferma esplicita dell'autore e carica la bozza privata completa di cover e metadati su Substack via MCP. |

---

## 📁 Struttura del Progetto

```text
.
├── .gitignore                      # Protezione chiavi, venv e file temporanei
├── README.md                       # Documentazione completa dell'infrastruttura
├── AGENTS.md                       # Master system prompt & orchestratore dei comandi
├── config/
│   ├── mcp_servers.json.example    # Esempio di configurazione dei server MCP
│   ├── style_guide.md              # Voce dell'autore, tono, blacklist ed estratti gold-standard
│   ├── visual_style.md             # Direttive estetiche, palette cromatica, negative prompt (per Art Director)
│   └── workflow_config.yaml        # Parametri globali (lingua, naming uscite, aspect ratio)
├── agents/                         # Moduli sub-agentici caricati dall'harness
│   ├── 00_bootstrap_profiler.md    # Setup: Profilazione stile e visual da Substack MCP
│   ├── 01_topic_scout.md           # Step 0: Ricerca trend + Substack read (DDG / Native)
│   ├── 02_sparring_partner.md      # Step 1: Analisi logica e critica della scaletta
│   ├── 03_copy_editor.md           # Step 2: Correzione bozza, refusi e ritmo
│   ├── 04_packaging_agent.md       # Step 3: Subject line, preview text e CTA
│   ├── 05_art_director.md          # Step 4: Direzione artistica, concept e generazione cover via Nano Banana MCP
│   └── 06_substack_publisher.md    # Step 5: Validazione e upload draft via Substack MCP
├── templates/                      # Scheletri standard dei checkpoint
│   ├── 00_pitch_template.md        # Formato per le 3 proposte di topic
│   ├── 01_outline_template.md      # Scaletta dell'autore a punti
│   ├── 02_draft_template.md        # Template prima stesura Markdown
│   └── 03_metadata_template.json   # Metadati per Substack (titoli, cover, slug)
├── drafts/                         # Workspace delle uscite (File-as-State pattern)
│   └── issue-NN/                   # Cartella della singola uscita (es. issue-01, issue-05)
│       ├── 00_pitches.md           # Proposte di topic (Topic Scout)
│       ├── 01_outline.md           # Scaletta a punti dell'autore
│       ├── 02_sparring.md          # Verbale di revisione e obiezioni (Sparring Partner)
│       ├── 03_draft.md             # Prima stesura completa dell'autore
│       ├── 04_review_diff.md       # Tabella diff con correzioni e refusi (Copy Editor)
│       ├── metadata.json           # Titoli, preview text, CTA e metadati cover
│       └── assets/                 # Asset multimediali dell'uscita
│           └── cover.png           # Copertina 16:9 generata dall'Art Director
└── .agents/
    ├── mcp_config.json             # Configurazione locale dei server MCP
    ├── workflows/                  # Flussi esecutivi invocati dai comandi slash
    │   ├── bootstrap.md
    │   ├── scout.md
    │   ├── sparring.md
    │   ├── review.md
    │   ├── package.md
    │   ├── cover.md                # Flusso dedicato alla rigenerazione visiva (Art Director)
    │   └── publish.md
    └── skills/                     # Skill native per Antigravity CLI (agy)
        ├── bootstrap/SKILL.md
        ├── scout/SKILL.md
        ├── sparring/SKILL.md
        ├── review/SKILL.md
        ├── package/SKILL.md
        ├── cover/SKILL.md          # Skill nativa cover (Art Director)
        └── publish/SKILL.md
```

---

## 🔌 Configurazione Server MCP

Il workflow si integra nativamente con 3 server MCP configurati in `.agents/mcp_config.json` (vedi template `config/mcp_servers.json.example`):

1. **`substack`:** Lettura dell'archivio, statistiche, upload asset e creazione di bozze private (usato da Bootstrap Profiler, Topic Scout e Publisher).
2. **`duckduckgo`:** Ricerca web a zero token per lo scouting di trend recenti (usato da Topic Scout, con fallback a tool nativi).
3. **`nano-banana`:** Generazione visiva delle immagini di copertina (utilizzato programmaticamente dall'**Art Director**).

### Esempio di configurazione (`.agents/mcp_config.json`):

```json
{
  "mcpServers": {
    "nano-banana": {
      "command": "npx",
      "args": ["-y", "nano-banana-mcp"],
      "env": {
        "GEMINI_API_KEY": "LA_TUA_GEMINI_API_KEY"
      }
    },
    "substack": {
      "command": "npx",
      "args": ["-y", "substack-mcp@latest"],
      "env": {
        "SUBSTACK_PUBLICATION_URL": "https://tua-pubblicazione.substack.com/",
        "SUBSTACK_SESSION_TOKEN": "IL_TUO_COOKIE_SUBSTACK_SESSION_TOKEN",
        "SUBSTACK_USER_ID": "IL_TUO_SUBSTACK_USER_ID"
      }
    },
    "duckduckgo": {
      "command": "uvx",
      "args": ["duckduckgo-mcp-server"]
    }
  }
}
```

> ⚠️ **Regola Inviolabile sull'Esecuzione MCP:** Tutte le interazioni con i servizi avvengono direttamente tramite tool MCP integrati (`call_mcp_tool`). È severamente vietato eseguire script intermedi (curl, script Python/Node.js ad hoc) per effettuare chiamate alle API esterne.
> 
> 🔒 **Sicurezza:** Non committare mai credenziali su Git. Il file `.gitignore` include già `.agents/mcp_config.json`.

---

## 🚀 Setup Iniziale Una Tantum (`/bootstrap`)

Prima di redigere nuovi numeri, istruisci la redazione a conoscere la tua voce e la tua identità visiva:

1. Avvia la CLI dell'agente nel workspace.
2. Invia il comando:
   ```text
   /bootstrap
   ```
   *(oppure in linguaggio naturale: "Analizza il mio archivio Substack e crea le guide di stile")*.
3. L'agente interrogherà Substack via MCP scaricando i tuoi post recenti e popolerà automaticamente:
   * `config/style_guide.md`: analisi del ritmo, uso dei pronomi, lessico ricorrente, blacklist cliché e 2 estratti gold-standard.
   * `config/visual_style.md`: palette cromatica, texture, stile artistico e negative prompt che guideranno l'**Art Director** in ogni uscita.

---

## 🔄 Il Ciclo Editoriale Passo-Passo (File-as-State)

Ogni nuova uscita vive in una cartella dedicata dentro `drafts/` (es. `drafts/issue-01/`, `drafts/issue-05/`):

```text
[0. Scouting] -> [1. Outline] -> [2. Sparring] -> [3. Stesura] -> [4. Review] -> [5. Packaging] -> [6. Art Direction] -> [7. Deploy Draft]
```

### 1. Scouting dei Trend (`/scout`)
* **Sub-Agente:** Topic Scout (`agents/01_topic_scout.md`)
* **Comando:** `/scout` *(o "Cerca argomenti per la prossima uscita")*
* **Cosa fa:** Crea la nuova cartella incrementale (es. `drafts/issue-06/`), mappa gli ultimi articoli su Substack per evitare duplicati, cerca novità e trend via web e genera `00_pitches.md` con 3 proposte editoriali complete di "Why Now" e bozza di scaletta.

### 2. Scrittura dell'Outline (Autore)
* **Chi agisce:** L'autore.
* **Cosa fa:** Copia `templates/01_outline_template.md` in `drafts/issue-NN/01_outline.md` e compila la propria tesi, l'angolo originale e i punti cardine dell'argomentazione.

### 3. Sparring Partner Logico (`/sparring`)
* **Sub-Agente:** Sparring Partner (`agents/02_sparring_partner.md`)
* **Comando:** `/sparring` *(o "Metti alla prova la mia scaletta")*
* **Cosa fa:** Analizza criticamente `01_outline.md` dialogando direttamente nella sessione. Solleva le 2 obiezioni più insidiose di un lettore scettico e segnala passaggi argomentativi deboli. Salva il verbale in `02_sparring.md`. **Regola ferrea:** Non riscrive mai l'outline al posto tuo.

### 4. Prima Stesura dell'Articolo (Autore)
* **Chi agisce:** L'autore.
* **Cosa fa:** Basandosi su scaletta e verbale di sparring, redige la prima bozza completa in `drafts/issue-NN/03_draft.md` con la propria voce naturale.

### 5. Copy Editing & Diff Review (`/review`)
* **Sub-Agente:** Copy Editor (`agents/03_copy_editor.md`)
* **Comando:** `/review` *(o "Correggi la bozza")*
* **Cosa fa:** Confronta `03_draft.md` con `config/style_guide.md`, individua refusi, frasi farraginose e cliché AI vietati ("nel panorama odierno", "crocevia"). Genera la tabella `04_review_diff.md` con proposte mirate di micro-intervento senza alterare il testo originale. L'autore applica le correzioni gradite.

### 6. Packaging Editoriale (`/package`)
* **Sub-Agente:** Packaging Specialist (`agents/04_packaging_agent.md`) + Art Director (`agents/05_art_director.md`)
* **Comando:** `/package` *(o "Prepara titoli e packaging")*
* **Cosa fa:** Analizza la bozza approvata e compila `metadata.json`:
  * 5 varianti di Subject Line (Curiosity Gap, Beneficio Diretto, Provocatoria, Contro-intuitiva, Minimalista).
  * 2 Preview Text (<90 caratteri per client email mobile).
  * Domanda/CTA per stimolare i commenti finali.
  * Invoca contestualmente l'Art Director per creare la prima copertina ufficiale in `assets/cover.png`.

### 7. Direzione Artistica & Creazione Copertina (`/cover`)
* **Sub-Agente:** Art Director & Visual Designer (`agents/05_art_director.md`)
* **Comando:** `/cover` *(o "Rigenera la copertina", "Cambia il visual")*
* **Cosa fa:** L'Art Director è il visual designer e prompt engineer dedicato:
  1. **Metafora Concettuale:** Legge `03_draft.md` ed estrae la metafora o l'oggetto fisico emblematico del pezzo (evitando interpretazioni letterali o banali).
  2. **Stile & Direttive:** Consulta `config/visual_style.md` per applicare la palette cromatica, la texture e lo stile editoriale concordato.
  3. **Vincoli Rigorosi:**
     * ⛔ **NO TEXT IN IMAGE:** Nessuna scritta, lettera, logo o titolo nell'immagine (evita caratteri alieni o sbavature).
     * ⛔ **NO CLICHÉ AI:** Banditi robot umanoidi, cervelli luminosi, nodi di rete cosmici e grafica stock aziendale.
     * 📐 **Formato 16:9:** Aspect ratio nativo per miniature e card social.
     * 🌐 **Prompt in Inglese:** Ottimizzato per modelli di diffusione visiva.
  4. **Generazione & Salvataggio:** Invoca Nano Banana MCP e salva l'asset in `drafts/issue-NN/assets/cover.png`.
  5. **Metadati:** Aggiorna `metadata.json` con `local_path`, `prompt_used` e un `alt_text` accessibile in italiano.
* *Nota:* Il comando `/cover` può essere invocato in qualsiasi momento per esplorare composizioni alternative senza toccare i titoli o i testi dell'articolo.

### 8. Validazione e Caricamento Bozza (`/publish`)
* **Sub-Agente:** Substack Publisher (`agents/06_substack_publisher.md`)
* **Comando:** `/publish` *(o "Carica la bozza su Substack")*
* **Cosa fa:** Sanitizza il Markdown per l'editor Substack, mostra un riepilogo dettagliato per approvazione esplicita (Human-in-the-Loop), effettua l'upload della copertina creata dall'Art Director e crea la **Bozza (Draft)** su Substack. Restituisce all'autore il link privato per l'anteprima online e l'invio finale manuale.

---

## 🛠️ Comandi Rapidi e Mapping dei Moduli

| Comando Rapido | Linguaggio Naturale Equivalente | Sub-Agente Esecutore | Input / Output Coinvolti |
| :--- | :--- | :--- | :--- |
| **`/bootstrap`** | *"Fai il setup dello stile"*, *"Analizza il mio archivio"* | `agents/00_bootstrap_profiler.md` | **In:** Substack MCP<br>**Out:** `config/style_guide.md`, `config/visual_style.md` |
| **`/scout`** | *"Cerca argomenti per il prossimo numero"*, *"Trova trend"* | `agents/01_topic_scout.md` | **In:** Web Search + Substack MCP<br>**Out:** `drafts/issue-NN/00_pitches.md` |
| **`/sparring`** | *"Fai da sparring sul mio outline"*, *"Critica la scaletta"* | `agents/02_sparring_partner.md` | **In:** `01_outline.md`<br>**Out:** Dialogo chat + `02_sparring.md` |
| **`/review`** | *"Correggi la bozza"*, *"Fai il copy editing"* | `agents/03_copy_editor.md` | **In:** `03_draft.md` + `style_guide.md`<br>**Out:** `04_review_diff.md` |
| **`/package`** | *"Prepara titoli e packaging"*, *"Fai il packaging"* | `agents/04_packaging_agent.md` + `agents/05_art_director.md` | **In:** `03_draft.md`<br>**Out:** `metadata.json` + `assets/cover.png` |
| **`/cover`** | *"Rigenera la copertina"*, *"Cambia il visual dell'uscita"* | `agents/05_art_director.md` *(Art Director)* | **In:** `03_draft.md` + `visual_style.md`<br>**Out:** `assets/cover.png` + `metadata.json` |
| **`/publish`** | *"Invia la bozza su Substack"*, *"Crea il draft online"* | `agents/06_substack_publisher.md` | **In:** `03_draft.md`, `metadata.json`, `assets/cover.png`<br>**Out:** Bozza (Draft) privata su Substack |

---

## 🎨 Focus: Come Lavora l'Art Director

L'**Art Director** (`agents/05_art_director.md`) garantisce che ogni uscita abbia una copertina originale e memorabile, lontana dalle grafiche generiche generate con prompt superficiali:

1. **Lettura Critica del Testo:** Non si limita a parole chiave, ma individua la metafora guida dell'articolo (es. un telaio tessile meccanico per rappresentare l'orchestrazione software, un'incudine moderna per il tool building artigianale).
2. **Ingegnerizzazione del Prompt secondo le Direttive:**
   Il prompt viene formulato in inglese secondo la struttura codificata:
   ```text
   [Descrizione scena e metafora concreta], [Stile artistico e tecnica da visual_style.md], [Palette cromatica e accenti di luce], [Inquadratura 16:9, spazio negativo, no text, no watermark, editorial aesthetic]
   ```
3. **Controllo di Qualità Visivo:**
   * Nessun testo impresso nell'immagine (evita caratteri alieni o sbavature).
   * Rispetto della palette identitaria della pubblicazione definita in `config/visual_style.md`.
   * Formato 16:9 pronto per l'upload tramite Substack MCP come header e social preview card.
