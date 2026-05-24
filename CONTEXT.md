# Project Memory

A skill for managing semi-persistent agent engineering memory across sessions. Uses a minimal document system (AGENTS.md, PROJECT_STATE.md, DECISIONS.md, RUNBOOK.md) to avoid long-conversation context bloat while preserving project progress, decisions, and task state.

## Behaviors

- **Setup**: One-time per project. Bootstrap the document system (AGENTS.md, PROJECT_STATE.md, DECISIONS.md, RUNBOOK.md, archive/). Invoked via `/setup-project-memory`. Session bootstrap and context freeze prompts are written into PROJECT_STATE.md for manual copy-paste use — they are not separate skill behaviors.
