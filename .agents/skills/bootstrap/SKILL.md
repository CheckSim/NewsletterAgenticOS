---
name: bootstrap
description: Esegue il setup iniziale una tantum profilando lo stile di scrittura e l'identità visiva della pubblicazione tramite Substack MCP.
---

# Bootstrap Skill

Questa skill attiva il sub-agente `agents/00_bootstrap_profiler.md`.

## Procedura
1. Leggi attentamente le istruzioni in `agents/00_bootstrap_profiler.md`.
2. Interroga Substack MCP per estrarre gli ultimi post pubblicati (secondo il conteggio in `config/workflow_config.yaml`).
3. Analizza la voce dell'autore ed estrai 2 estratti gold-standard per `config/style_guide.md`.
4. Analizza l'identità visiva e la palette per `config/visual_style.md`.
5. Presenta all'autore una sintesi nel terminale e chiedi conferma delle impostazioni.
