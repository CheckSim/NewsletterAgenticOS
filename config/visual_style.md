# Guida allo Stile Visivo e Direzione Artistica (Visual Style Guide)

> **Nota:** Questo file definisce l'identità grafica delle copertine e degli asset visivi della newsletter.
> Può essere aggiornato automaticamente tramite il comando `/bootstrap` (analizzando le cover storiche via Substack MCP) oppure raffinato a mano dall'autore.

---

## 1. Visione Estetica e Stile Artistico
* **Stile Generale:** Editoriale, concettuale, moderno, sobrio. Preferenza per grafica vettoriale pulita, xilografia contemporanea, illustrazione concettuale o fotografia d'autore ad alto contrasto.
* **Mood:** Pragmatico, stimolante, tech-humanist, artigianato digitale.
* **Composizione:** Rapporto d'aspetto **16:9**. Spazi negativi ampi, soggetto focale chiaro e non sovraffollato, adatto al layout responsive delle email e del web feed di Substack.

---

## 2. Palette Cromatica di Riferimento
* **Colore Primario:** Antracite scuro / Nero profondo (`#111827`)
* **Colore Secondario:** Bianco caldo / Carta naturale (`#F9FAFB`)
* **Accento Principale:** Blu cobalto o Ottanio sobrio (`#0284C7` / `#0F766E`)
* **Accento Secondario (Opzionale):** Arancio ambra caldo (`#D97706`)

---

## 3. Regole di Prompting (in lingua inglese per generatori visivi)
Ogni prompt generato da `05_art_director.md` deve seguire la seguente anatomia:
1. **Soggetto e Metafora:** Descrizione tangibile di un oggetto, scena o interazione che incarna la metafora dell'articolo (es. *"an artisan calibrating a mechanical balance clock"* anziché *"artificial intelligence"*).
2. **Stile & Tecnica:** Specificare il mezzo (es. *"editorial vector illustration, subtle grain texture, matte colors, minimalist graphic design style"*).
3. **Illuminazione e Colore:** Richiamare la palette specifica (es. *"deep charcoal and warm cream palette with subtle electric blue accents"*).
4. **Inquadratura:** *"Clean 16:9 composition, centered focus with breathing negative space"*.

---

## 4. Negative Prompt & Cose da Evitare Assolutamente
Includere sempre o forzare implicitamente l'esclusione di:
* ⛔ **Niente Testo:** Nessuna parola, lettera, titolo, watermark, firma o tipografia nell'immagine generata.
* ⛔ **Niente Cliché AI:** Cervelli fluorescenti, robot cromati, ologrammi azzurri con fasci di luce, mani robotiche che toccano mani umane, reticoli digitali generici.
* ⛔ **Niente 3D Plastico:** Evitare render lucidi stile stock 3D corporate / cartoon generico.
* ⛔ **Niente Sovraffollamento:** Evitare composizioni caotiche con troppi dettagli non correlati.
