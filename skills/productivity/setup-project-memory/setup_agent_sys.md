请为当前项目建立一套"短 session + 强外部记忆"的基础版半持久化 Agent 工程系统。

重要要求：
本次只建设基础版，不要配置 hooks，不要配置 automation，不要创建复杂协议目录，不要创建大量分散文档。

目标：
用最少的项目文档承载 Codex 长周期开发所需的外部记忆，避免长对话上下文膨胀，同时避免文档系统本身继续熵增。

核心原则：

1. 对话上下文是临时工作区，不是长期记忆。
2. AGENTS.md 只保存长期稳定工程规则。
3. docs/project_state/PROJECT_STATE.md 保存当前项目状态和下一步任务。
4. docs/project_state/DECISIONS.md 保存长期工程决策。
5. docs/project_state/RUNBOOK.md 保存运行、测试、恢复方式。
6. archive/ 只保存历史记录，默认新 session 不读取。
7. 不创建过多协议文件。
8. 不把临时聊天内容写入长期文档。
9. 不编造不存在的文件、脚本、运行结果或测试结果。
10. 如果信息不足，明确写 TODO / UNKNOWN / NEEDS_VERIFICATION。

---

# 一、创建最小目录结构

请创建或更新：

- docs/project_state/
- docs/project_state/archive/

不要创建复杂子目录，除非当前项目已经存在且确实有必要复用。

---

# 二、创建或更新 AGENTS.md

AGENTS.md 只保存长期稳定规则。

允许包含：

- 项目背景
- 编码规范
- 目录规范
- 日志规范
- 输出规范
- 测试规范
- 大文件处理约束
- 长任务处理约束
- 错误处理规范
- 禁止行为
- project_state 文档入口说明

必须包含：

"项目状态、下一步任务、checkpoint、handoff、context freeze 记录均维护在 docs/project_state/PROJECT_STATE.md 中；AGENTS.md 只保存长期稳定工程规则。"

禁止写入：

- 临时聊天内容
- session-specific 状态
- 短期 TODO
- 运行日志
- 任务历史流水账
- 过长项目总结

---

# 三、创建或更新 docs/project_state/PROJECT_STATE.md

这是最核心的状态文件。

请使用以下固定结构：

## 1. New Session Bootstrap

写入新 session 最短启动语句：

"请阅读 AGENTS.md 和 docs/project_state/PROJECT_STATE.md，然后按其中流程恢复项目状态，继续 Current Next Task 中标记的最高优先级且无 blocker 的任务。不要重新设计整个系统，除非发现文档与代码严重冲突。"

同时说明：

- 新 session 先读 AGENTS.md
- 再读 PROJECT_STATE.md
- 只有需要架构决策时才读 DECISIONS.md
- 只有需要运行、测试、部署时才读 RUNBOOK.md
- 不要一开始扫描整个仓库
- 不要重新设计已完成部分

---

## 2. Project Snapshot

总结：

- 当前项目目标
- 当前项目阶段
- 已完成工作
- 未完成工作
- 当前系统 / pipeline 概况
- 当前关键文件
- 当前关键目录
- 当前风险点
- 当前状态可信度：CONFIRMED / PARTIAL / STALE / UNKNOWN
- 最近更新时间

要求：
这是当前项目状态快照，不是聊天记录。

---

## 3. Current Next Task

必须明确写出：

- 当前最高优先级且无 blocker 的任务
- 为什么它是下一步
- 完成标准
- 相关文件
- 如果没有明确任务，写 NEEDS_TRIAGE

---

## 4. Task Queue

用 checklist 维护任务。

每个任务包含：

- Task ID
- 任务名称
- 状态：TODO / IN_PROGRESS / BLOCKED / DONE
- 优先级：P0 / P1 / P2 / P3
- blocker
- 完成标准
- 相关文件

任务选择规则：

1. 优先继续 IN_PROGRESS。
2. 其次选择最高优先级 TODO。
3. BLOCKED 任务不能执行。
4. DONE 任务不要重复做。
5. 如果文档和代码冲突，先标记 NEEDS_VERIFICATION。

---

## 5. Checkpoint

记录当前长任务或阶段性任务状态。

包含：

- Active Task
- Status：RUNNING / COMPLETED / FAILED / STALLED / UNKNOWN / NONE
- Last Check Time
- Input Path
- Output Path
- Log Path
- Progress Indicator
- Last Successful Step
- Current Error
- Recovery Suggestion

如果没有长任务，明确写：

"当前没有 active long-running task。"

---

## 6. Known Issues

记录当前已知问题。

每个问题包含：

- Issue ID
- Severity：Critical / High / Medium / Low
- Status：Open / Investigating / Resolved
- Description
- Impact
- Suggested next action

---

## 7. Handoff Notes

写给新 session / 新 agent 的接手说明：

- 当前做到哪一步
- 接手后第一件事是什么
- 哪些内容不要重新讨论
- 哪些内容需要验证
- 当前 blocker
- 当前风险点

---

## 8. Context Freeze Rule

在本文件中直接定义 context freeze，不再单独创建协议文件。

请写明：

Context Freeze 不是 Codex 内置功能，而是本项目定义的手动工程动作。

定义：
当上下文过长、准备切换 session、阶段性任务完成、长任务开始或结束时，将当前隐含在聊天中的项目状态外化到 AGENTS.md、PROJECT_STATE.md、DECISIONS.md、RUNBOOK.md 中。

触发时机：

- 上下文即将过长
- 准备开启新 session
- compact 前
- 阶段性任务完成后
- 长任务开始前或结束后
- 用户要求"总结当前进展"

执行步骤：

1. 更新 PROJECT_STATE.md
2. 如有新稳定决策，更新 DECISIONS.md
3. 如有运行方式变化，更新 RUNBOOK.md
4. 如有长期规则变化，更新 AGENTS.md
5. 必要时在 archive/ 保存本次 freeze 摘要
6. 输出新 session 最短启动语句

禁止：

- 不重构业务代码
- 不编造运行结果
- 不写入临时聊天
- 不把短期 TODO 写入 AGENTS.md
- 不创建新的机制文件，除非用户明确要求

---

## 9. Manual Context Freeze Prompt

保存这个可直接复制的短命令：

"请执行一次 context freeze：只更新 AGENTS.md、docs/project_state/PROJECT_STATE.md、docs/project_state/DECISIONS.md、docs/project_state/RUNBOOK.md。不要重构业务代码。完成后输出修改文件列表、当前最高优先级无 blocker 任务、新 session 最短启动语句。"

---

## 10. Update Log

只记录重要更新摘要。

格式：

- Time
- Trigger
- Updated files
- Summary
- Verification status

不要记录完整聊天内容。

---

# 四、创建或更新 docs/project_state/DECISIONS.md

用途：
只记录重要长期工程决策，不记录普通 TODO。

每条 decision 使用轻量 ADR 格式：

- Decision ID
- Date
- Status：Accepted / Deprecated / Superseded / Proposed
- Context
- Decision
- Rationale
- Consequences
- Related files

要求：

- 只记录真正影响架构、数据流、运行方式、性能、可靠性、目录结构的决策
- 不记录临时讨论
- 不记录普通实现细节
- 如果某条决策过期，标记 Deprecated 或 Superseded，不要直接删除

---

# 五、创建或更新 docs/project_state/RUNBOOK.md

用途：
记录如何运行、测试、查看输出和恢复。

必须包含：

- 环境准备
- 依赖安装
- 主要运行命令
- 测试命令
- 日志位置
- 输出位置
- 如何判断成功
- 如何判断失败
- 如何恢复
- 当前未知项

如果信息不足，写 TODO / UNKNOWN，不要编造。

---

# 六、归档规则

archive/ 只用于保存历史状态。

要求：

- archive/ 默认不作为新 session 必读内容
- PROJECT_STATE.md 只保存当前状态，不保存完整历史
- 旧状态可归档到 archive/
- 不要让 archive/ 参与日常上下文恢复
- 不要因为归档创建复杂目录层级

---

# 七、文档与代码一致性检查

更新文档前，请尽量检查：

- 文档提到的关键文件是否真实存在
- 文档提到的命令是否仍然有效
- 文档提到的输出目录是否存在或合理
- 当前任务是否与代码状态一致
- 是否存在文档过期

如果无法验证，请写 NEEDS_VERIFICATION，不要假设。

---

# 八、最后执行一次基础 context freeze

完成文档体系创建后，请立即执行一次基础 context freeze。

要求：

- 更新 AGENTS.md
- 更新 docs/project_state/PROJECT_STATE.md
- 更新 docs/project_state/DECISIONS.md
- 更新 docs/project_state/RUNBOOK.md
- 必要时在 archive/ 写入本次 freeze 摘要
- 不重构业务代码
- 不创建 hooks
- 不创建 automation
- 不创建额外协议文件

---

# 九、最后输出报告

完成后请输出：

1. 新增文件列表
2. 修改文件列表
3. 当前文档体系说明
4. 当前最高优先级且无 blocker 的任务
5. 当前 active long-running task 状态
6. 当前缺失信息
7. 是否发现文档与代码不一致
8. 新 session 最短启动语句
9. 手动 context freeze 短命令

再次强调：
本次是收敛版基础系统。
不要创建 hooks。
不要创建 automation。
不要创建大量 protocol 文档。
不要把文档系统本身复杂化。
优先保证简单、稳定、可恢复。
