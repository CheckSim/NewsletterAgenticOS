---
name: package
description: Ottimizza il packaging della bozza (5 subject line, preview text, CTA) in metadata.json e genera la copertina con Nano Banana MCP in assets/cover.png.
---

# Package Skill

Questa skill attiva `agents/04_packaging_agent.md` e `agents/05_art_director.md`.

## Procedura
1. Leggi attentamente le istruzioni in `agents/04_packaging_agent.md` e `agents/05_art_director.md`.
2. Individua l'uscita attiva e leggi `drafts/issue-NN/03_draft.md`.
3. Formula 5 subject line, 2 opzioni di preview text (<90 caratteri) e la CTA finale; salvali in `metadata.json`.
4. Estrai la metafora visiva e formula il prompt descrittivo in inglese secondo `config/visual_style.md`.
5. Invoca Nano Banana MCP (o tool nativo) per generare `drafts/issue-NN/assets/cover.png` (16:9).
6. Mostra le opzioni all'autore e chiedi quale titolo impostare come predefinito.
