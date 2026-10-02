---
name: review
description: Esegue il copy editing della prima bozza (03_draft.md), caccia refusi e cliché AI, e genera la tabella diff in 04_review_diff.md.
---

# Review Skill

Questa skill attiva il sub-agente `agents/03_copy_editor.md`.

## Procedura
1. Leggi attentamente le istruzioni in `agents/03_copy_editor.md`.
2. Individua l'uscita attiva e leggi `drafts/issue-NN/03_draft.md` e `config/style_guide.md`.
3. Individua refusi, periodi involuti e violazioni della blacklist dei cliché AI.
4. Genera la tabella dettagliata dei micro-interventi in `drafts/issue-NN/04_review_diff.md`.
5. Non modificare direttamente `03_draft.md`; lascia all'autore l'accettazione dei suggerimenti.
