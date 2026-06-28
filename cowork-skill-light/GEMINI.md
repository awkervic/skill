# Project Instructions

## AICloud Lite

本项目使用 patch-based multi-agent state machine。

核心规则：

1. `cowork/state.md` 是唯一真相。
2. 任意 agent 只能读取 `cowork/state.md`。
3. 任意 agent 只能输出 `cowork/patch.json`。
4. agent 不允许直接修改 `cowork/state.md`。
5. merge engine 负责合并 patch 并更新 state。
6. 禁止角色绑定，支持 opencode / codex / any LLM。

## 文件结构

```text
cowork/
├── state.md
└── patch.json
```

## 流程

1. 读取 `state.md`。
2. 执行任务。
3. 生成 `patch.json`。
4. merge engine 应用 patch。
5. overwrite 更新 `state.md`。

禁止 logs、history、neat、长期记录文件。
