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

### 3. powershell-safe-invocation

目录：[`powershell-safe-invocation/`](./powershell-safe-invocation/)

Windows PowerShell 安全调用与文件操作规范，涵盖原生命令参数、路径转义、进程启动、脚本执行和文件系统变更。

### 4. anthropics/skills 文档技能

以下技能来自 [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills)：

- [`docx/`](./docx/)：Word 文档创建、读取与编辑。
- [`pdf/`](./pdf/)：PDF 文件处理。
- [`pptx/`](./pptx/)：PowerPoint 演示文稿处理。
- [`xlsx/`](./xlsx/)：Excel 电子表格处理。

## 使用方式

在支持 Skills 的 AI CLI 工具中加载本仓库或相关目录。每个技能目录包含：

- `SKILL.md`: 通用技能描述与执行 SOP。
- `CLAUDE.md`: Claude Code 适配指令。
- `GEMINI.md`: Gemini / Antigravity 适配指令。
