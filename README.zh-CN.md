# Project Memory

[English](./README.md) | [中文](./README.zh-CN.md)

一个用于搭建半持久化 Agent 工程记忆系统的 skill。通过最小化文档体系避免长对话上下文膨胀，同时保留项目进度、决策和任务状态。

## 安装

```bash
npx skills add RouVen-crp/project-memory
```

根据提示选择要安装的 skill。

## 使用

每个项目执行一次：

```
/setup-project-memory
```

Agent 会创建以下文档体系：

- `AGENTS.md` — 长期稳定的工程规则
- `docs/project_state/PROJECT_STATE.md` — 当前项目状态和任务队列
- `docs/project_state/DECISIONS.md` — 架构和工程决策
- `docs/project_state/RUNBOOK.md` — 运行、测试和恢复方式
- `docs/project_state/archive/` — 历史快照（新 session 默认不读取）

## 安装后

### 启动新 Session

```
/resume-project
```

读取 AGENTS.md + PROJECT_STATE.md，恢复项目状态并继续最高优先级的无阻塞任务。

### 冻结上下文

```
/context-freeze
```

将聊天中的项目状态外化到文档系统，不修改业务代码。

上下文冻结建议在上下文窗口使用到达160k左右使用

## 许可证

MIT
