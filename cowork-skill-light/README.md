# AICloud Lite

AICloud Lite 是一个 patch-based multi-agent state machine。

核心规则：

- `cowork/state.md` 是唯一真相。
- 任意 agent 只能读取 `cowork/state.md`。
- 任意 agent 只能输出 `cowork/patch.json`。
- agent 不允许直接修改 `state.md`。
- merge engine 负责合并 `patch.json` 并更新 `state.md`。
- 禁止 logs、history、neat、长期记录文件。
- 禁止角色绑定，支持 opencode / codex / any LLM。

## 文件结构

```text
cowork/
├── state.md
└── patch.json
```

## 流程

1. 读取 `state.md`
2. 任意 agent 执行任务
3. 生成 `patch.json`
4. merge engine 应用 patch
5. overwrite 更新 `state.md`
