---
name: cover
description: Rigenera esclusivamente l'immagine di copertina (assets/cover.png) tramite Nano Banana MCP senza modificare testi o metadati.
---

# Cover Skill

Questa skill attiva il sub-agente `agents/05_art_director.md`.

## Procedura
1. Leggi attentamente le istruzioni in `agents/05_art_director.md`.
2. Individua l'uscita attiva e leggi `drafts/issue-NN/03_draft.md` e `config/visual_style.md`.
3. Formula un nuovo prompt descrittivo in inglese per esplorare un angolo o una composizione alternativa (16:9, no text, no cliché AI).
4. Invoca Nano Banana MCP per sovrascrivere o salvare la nuova cover in `drafts/issue-NN/assets/cover.png`.
5. Aggiorna `metadata.json` con il nuovo prompt utilizzato e presenta il risultato all'autore.
