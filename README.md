# Project Memory

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

Copy-paste this prompt into a fresh chat:

> 请阅读 AGENTS.md 和 docs/project_state/PROJECT_STATE.md，然后按其中流程恢复项目状态，继续 Current Next Task 中标记的最高优先级且无 blocker 的任务。不要重新设计整个系统，除非发现文档与代码严重冲突。

### Freeze Context

When context gets long, copy-paste:

> 请执行一次 context freeze：只更新 AGENTS.md、docs/project_state/PROJECT_STATE.md、docs/project_state/DECISIONS.md、docs/project_state/RUNBOOK.md。不要重构业务代码。完成后输出修改文件列表、当前最高优先级无 blocker 任务、新 session 最短启动语句。

## License

MIT
