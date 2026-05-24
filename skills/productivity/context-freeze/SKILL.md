---
name: context-freeze
description: Freeze the current conversation context into the projects external memory docs. Updates AGENTS.md, PROJECT_STATE.md, DECISIONS.md, and RUNBOOK.md without modifying business code.
---

# Context Freeze

请执行一次 context freeze：只更新 AGENTS.md、docs/project_state/PROJECT_STATE.md、docs/project_state/DECISIONS.md、docs/project_state/RUNBOOK.md。不要重构业务代码。完成后输出修改文件列表、当前最高优先级无 blocker 任务、新 session 最短启动语句。
