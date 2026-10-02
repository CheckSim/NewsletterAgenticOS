---
name: publish
description: Valida e sanitizza la bozza, richiede conferma esplicita all'autore e carica il draft completo su Substack tramite MCP.
---

# Publish Skill

Questa skill attiva il sub-agente `agents/06_substack_publisher.md`.

## Procedura
1. Leggi attentamente le istruzioni in `agents/06_substack_publisher.md`.
2. Verifica che `03_draft.md`, `metadata.json` (con titolo scelto) e `assets/cover.png` siano pronti.
3. Sanitizza il Markdown rimuovendo artefatti non compatibili con Substack.
4. Mostra all'autore il riquadro di riepilogo pre-deploy e richiedi conferma esplicita (Human-in-the-Loop).
5. Invoca Substack MCP per caricare la cover e creare la nuova Bozza (Draft) privata.
6. Salva l'ID e l'URL in `metadata.json` e restituisci il link privato all'autore.
