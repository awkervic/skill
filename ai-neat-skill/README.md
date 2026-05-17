# AI Neat Skill (AI 编年史记忆剪枝技能)

这是一个用于大模型 CLI 工具（如 Gemini CLI、Claude Code）的无损记忆管理流。

## 项目结构

- `SKILL.md`: 技能定义文件，包含了 AI 运行激活协议和执行细节。
- `memory.md`: 核心事件快照存储文件。

## 如何激活

当你在此项目中工作时，AI 会根据 `SKILL.md` 中的协议，在上下文过长时自动执行记忆压缩和剪枝，将重要事件记录到 `memory.md` 中。
