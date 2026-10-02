---
name: scout
description: Inizializza una nuova uscita in drafts/ e cerca trend e argomenti recenti proponendo 3 pitch editoriali con scaletta embrionale.
---

# Scout Skill

Questa skill attiva il sub-agente `agents/01_topic_scout.md`.

## Procedura
1. Leggi attentamente le istruzioni in `agents/01_topic_scout.md`.
2. Determina la cartella della nuova uscita (es. `drafts/issue-01/` o incrementale) e creala.
3. Consulta lo storico recente di Substack via MCP per escludere argomenti già trattati.
4. Esegui la ricerca di trend e news recenti (ultimi 30 giorni) via DuckDuckGo MCP o web search nativa.
5. Compila `drafts/issue-NN/00_pitches.md` con 3 pitch dettagliati e mostra una sintesi all'autore.
