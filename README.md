# Project Memory

[English](./README.md) | [中文](./README.zh-CN.md)

A skill for setting up a semi-persistent agent engineering memory system. Uses minimal documentation to avoid context window bloat across long sessions while preserving project progress, decisions, and task state.

## Install

```bash
npx skills add RouVen-crp/project-memory
```

Select the skill when prompted.

## Usage

Run once per project:

```
/setup-project-memory
```

The agent will create a document system:

- `AGENTS.md` — long-term stable engineering rules
- `docs/project_state/PROJECT_STATE.md` — current project state and task queue
- `docs/project_state/DECISIONS.md` — architecture and engineering decisions
- `docs/project_state/RUNBOOK.md` — how to run, test, and recover
- `docs/project_state/archive/` — historical snapshots (not read by new sessions)

## After Setup

### Start a New Session

```
/resume-project
```

Reads AGENTS.md + PROJECT_STATE.md and resumes the highest-priority unblocked task.

### Freeze Context

```
/context-freeze
```

Externalizes chat state to the document system without modifying business code.

It is recommened to freeze context once the context reaches around 160k

## License

MIT
