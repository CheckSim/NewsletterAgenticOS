# Substack Agentic Editorial Workflow ✍️🤖

Un repository modulare e pronto all'uso per trasformare qualsiasi assistente AI a riga di comando (**Antigravity CLI**, Claude Code, Hermes, Cursor) in una **redazione editoriale aumentata** per la tua pubblicazione Substack.

Basato sul pattern **Agent-Native Workspace (File-as-State)**: nessuna pipeline rigida in script monolitici, ma una collaborazione continua tra autore e intelligenza artificiale direttamente all'interno della sessione di lavoro.

---

## 🏛️ Filosofia: Human-Centric Editorial Board

1. **Zero Ghostwriting:** L'AI non genera mai articoli da zero né si sostituisce alla voce autentica dell'autore.
2. **Critique & Support First:** Gli agenti agiscono come compagni di redazione: ricercatori di trend, sparring partner logici, revisori di refusi, visual designer ed esecutori tecnici.
3. **Human-in-the-Loop Obbligatorio:** L'autore scrive la scaletta (`01_outline.md`) e la prima bozza completa (`03_draft.md`). L'agente interviene per stimolare la riflessione, validare la tenuta logica, correggere i cliché e confezionare la pubblicazione.
4. **Deploy Solo Bozza (Draft Only):** Nessun invio automatico a sorpresa. Il workflow si conclude sempre con il caricamento di una **bozza privata (draft)** su Substack, fornendo il link diretto per la preview finale prima dell'invio manuale agli iscritti.

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
│   ├── visual_style.md             # Direttive estetiche, palette cromatica, negative prompt
│   └── workflow_config.yaml        # Parametri globali (lingua, naming uscite, aspect ratio)
├── agents/                         # Moduli sub-agentici caricati dall'harness
│   ├── 00_bootstrap_profiler.md    # Setup: Profilazione stile e visual da Substack MCP
│   ├── 01_topic_scout.md           # Step 0: Ricerca trend + Substack read (DDG / Native)
│   ├── 02_sparring_partner.md      # Step 1: Analisi logica e critica della scaletta
│   ├── 03_copy_editor.md           # Step 2: Correzione bozza, refusi e ritmo
│   ├── 04_packaging_agent.md       # Step 3: Subject line, preview text e CTA
│   ├── 05_art_director.md          # Step 4: Concept visivo + Nano Banana MCP call
│   └── 06_substack_publisher.md    # Step 5: Validazione e upload draft via Substack MCP
├── templates/                      # Scheletri standard dei checkpoint
│   ├── 00_pitch_template.md        # Formato per le 3 proposte di topic
│   ├── 01_outline_template.md      # Scaletta dell'autore a punti
│   ├── 02_draft_template.md        # Template prima stesura Markdown
│   └── 03_metadata_template.json   # Metadati per Substack (titoli, cover, slug)
├── drafts/                         # Workspace delle uscite (File-as-State)
│   └── .gitkeep
└── .agents/
    └── skills/                     # Skill native per Antigravity CLI (agy)
        ├── bootstrap/SKILL.md
        ├── scout/SKILL.md
        ├── sparring/SKILL.md
        ├── review/SKILL.md
        ├── package/SKILL.md
        ├── cover/SKILL.md
        └── publish/SKILL.md
```

---

## 🔌 Configurazione Server MCP

Il workflow si integra con 3 server MCP. Configurali all'interno del tuo file di configurazione MCP (es. `.agents/mcp_config.json`):

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

> ⚠️ **Sicurezza:** Non committare mai su GitHub file contenenti token o chiavi private. `.gitignore` è già configurato per ignorare `.agents/mcp_config.json`. Usa `config/mcp_servers.json.example` come template pulito.

---

## 🚀 Setup Iniziale Una Tantum (`/bootstrap`)

Prima di redigere nuovi articoli, istruisci il sistema a conoscere la tua voce e la tua identità visiva:

1. Avvia la CLI dell'agente nel workspace.
2. Invia il comando:
   ```text
   /bootstrap
   ```
   *(oppure in linguaggio naturale: "Analizza il mio archivio Substack e crea le guide di stile")*.
3. L'agente interrogherà Substack MCP scaricando i tuoi post recenti e popolerà automaticamente:
   * `config/style_guide.md`: analisi del ritmo, uso dei pronomi, lessico ricorrente, blacklist cliché e 2 estratti gold-standard.
   * `config/visual_style.md`: palette cromatica, stile delle illustrazioni e parametri di prompt per le copertine.

---

## 🔄 Il Ciclo Editoriale Passo-Passo (File-as-State)

Ogni nuova uscita vive in una cartella dedicata dentro `drafts/` (es. `drafts/issue-01/`, `drafts/issue-02/`):

```text
[0. Scouting] -> [1. Outline] -> [2. Sparring] -> [3. Stesura] -> [4. Review] -> [5. Packaging & Visual] -> [6. Deploy Draft]
```

### 1. Scouting dei Trend (`/scout`)
* **Comando:** `/scout` *(o "Cerca argomenti per la prossima uscita")*
* **Cosa fa:** Crea la nuova cartella (es. `drafts/issue-01/`), legge gli ultimi articoli pubblicati su Substack per non ripetersi, cerca le novità recenti via web e genera `00_pitches.md` con 3 proposte editoriali complete di "Why Now" e bozza di scaletta.

### 2. Scrittura dell'Outline (Autore)
* **Chi agisce:** L'autore.
* **Cosa fa:** Copia `templates/01_outline_template.md` in `drafts/issue-NN/01_outline.md` e compila la propria tesi e i punti chiave dell'argomentazione.

### 3. Sparring Partner Logico (`/sparring`)
* **Comando:** `/sparring` *(o "Metti alla prova la mia scaletta")*
* **Cosa fa:** L'agente analizza `01_outline.md` e dialoga con te nella sessione, sollevando le 2 obiezioni principali di un lettore scettico e segnalando salti logici. Salva il verbale in `02_sparring.md`. **Regola ferrea:** Non riscrive mai l'outline al posto tuo.

### 4. Prima Stesura dell'Articolo (Autore)
* **Chi agisce:** L'autore.
* **Cosa fa:** Basandosi su scaletta e verbale di sparring, scrive la prima bozza completa in `drafts/issue-NN/03_draft.md` nel proprio stile naturale.

### 5. Copy Editing & Diff Review (`/review`)
* **Comando:** `/review` *(o "Correggi la bozza")*
* **Cosa fa:** L'agente confronta `03_draft.md` con `config/style_guide.md`, individua refusi e cliché vietati e genera la tabella `04_review_diff.md` con proposte di micro-intervento senza alterare il testo originale. L'autore applica le correzioni approvate.

### 6. Packaging & Cover Visual (`/package` e `/cover`)
* **Comando:** `/package` *(o "Prepara titoli e copertina")*
* **Cosa fa:** Genera in `metadata.json` 5 varianti di Subject Line (Curiosity Gap, Beneficio Diretto, Provocatoria, Contro-intuitiva, Minimalista), 2 Preview Text (<90 caratteri) e la CTA finale. Invoca l'Art Director per generare la copertina 16:9 con Nano Banana MCP in `assets/cover.png`.
* *Nota:* Per ritoccare o rigenerare esclusivamente l'immagine senza toccare i titoli, puoi usare in qualsiasi momento il comando rapido `/cover`.

### 7. Validazione e Caricamento Bozza (`/publish`)
* **Comando:** `/publish` *(o "Carica la bozza su Substack")*
* **Cosa fa:** Sanitizza il Markdown, mostra un riquadro di conferma con tutti i dati (Human-in-the-Loop), effettua l'upload della cover e crea la **Bozza (Draft)** su Substack. Restituisce all'autore il link privato per la rilettura finale pre-invio.

---

## 🛠️ Comandi Rapidi Supportati

| Comando | Descrizione Sintetica |
| :--- | :--- |
| `/bootstrap` | Setup una tantum: estrazione stile e visual dall'archivio Substack |
| `/scout` | Inizializza nuova uscita e propone 3 pitch con fonti fresche |
| `/sparring` | Revisione socratica dell'outline e salvataggio in `02_sparring.md` |
| `/review` | Caccia a refusi e cliché AI con tabella `04_review_diff.md` |
| `/package` | Packaging titoli, preview text e generazione cover 16:9 |
| `/cover` | Rigenerazione indipendente della sola copertina visiva |
| `/publish` | Validazione, conferma ed invio come bozza (Draft) su Substack |
