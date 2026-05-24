# Project Memory

A skill for managing semi-persistent agent engineering memory across sessions. Uses a minimal document system (AGENTS.md, PROJECT_STATE.md, DECISIONS.md, RUNBOOK.md) to avoid long-conversation context bloat while preserving project progress, decisions, and task state.

## Behaviors

Three manually-triggered skills:

- **Setup** (`/setup-project-memory`): One-time per project. Bootstrap the document system.
- **Resume** (`/resume-project`): Each new session. Read AGENTS.md + PROJECT_STATE.md and resume the highest-priority unblocked task.
- **Freeze** (`/context-freeze`): On demand. Externalize chat state into the document system without modifying business code.
