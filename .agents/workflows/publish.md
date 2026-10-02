---
description: Valida la bozza, richiede conferma esplicita e carica il draft completo su Substack tramite MCP
---

# /publish Workflow

Leggi ed esegui attentamente le istruzioni operative descritte in [agents/06_substack_publisher.md](../../agents/06_substack_publisher.md).
1. Sanitizza il Markdown di `03_draft.md` e verifica `metadata.json` e `assets/cover.png`.
2. Mostra il riquadro di conferma pre-deploy (Human-in-the-Loop) e attendi l'assenso dell'autore.
3. Carica la cover image e crea la Bozza (Draft) privata su Substack via MCP.
4. Salva i dettagli della draft in `metadata.json` e restituisci il link di anteprima online.
