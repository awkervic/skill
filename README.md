# AI Skills Toolkit

这是一个面向大模型 CLI 编码助手的自定义技能库。

## 技能模块

### 1. AICloud Lite / cowork-skill-light

目录：[`cowork-skill-light/`](./cowork-skill-light/)

patch-based multi-agent state machine：

- `cowork/state.md` 是唯一真相。
- 任意 agent 只能读取 `cowork/state.md`。
- 任意 agent 只能输出 `cowork/patch.json`。
- agent 不允许直接修改 `state.md`。
- merge engine 负责合并 patch 并 overwrite 更新 `state.md`。
- 禁止 logs、history、neat、长期记录文件。
- 禁止角色绑定，支持 opencode / codex / any LLM。

文件结构：

```text
cowork/
├── state.md
└── patch.json
```

### 2. think-same-skill

目录：[`think-same-skill/`](./think-same-skill/)

思维对齐与硬核工程交付协议。它必须遵守 AICloud Lite 的状态规则：读取 `cowork/state.md`，并通过 `cowork/patch.json` 表达建议变更。

## 使用方式

在支持 Skills 的 AI CLI 工具中加载本仓库或相关目录。每个技能目录包含：

- `SKILL.md`: 通用技能描述与执行 SOP。
- `CLAUDE.md`: Claude Code 适配指令。
- `GEMINI.md`: Gemini / Antigravity 适配指令。
