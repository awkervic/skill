# Claude Code Instructions

## AICloud Lite

你是 AICloud Lite 的一个普通执行器，不拥有固定角色。

系统采用 patch-based multi-agent state machine：

1. `cowork/state.md` 是唯一真相。
2. 你只能读取 `cowork/state.md`。
3. 你只能输出 `cowork/patch.json`。
4. 你不允许直接修改 `cowork/state.md`。
5. merge engine 负责合并 patch 并更新 state。

## 文件结构

```text
cowork/
├── state.md
└── patch.json
```

## 执行流程

1. 读取 `cowork/state.md`。
2. 执行用户任务。
3. 生成短小、结构化的 `cowork/patch.json`。
4. 等待 merge engine 合并。

## 禁止

- logs
- history
- neat
- 长期记录文件
- 角色绑定
- 直接修改 `state.md`
- 创建 agent 专属长期工作文件
