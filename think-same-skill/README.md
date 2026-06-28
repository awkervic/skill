# think-same-skill (思维对齐与硬核交付协议)

这是一个用于大模型 CLI 工具（如 Gemini CLI、Claude Code）的思维对齐与工程质量保障协议。

## 项目结构

- `SKILL.md`: 技能定义文件，包含了核心运行协议、记忆同步和工程交付红线。
- `GEMINI.md`: Gemini CLI 的激活与约束配置。
- `CLAUDE.md`: Claude Code 的项目指令。

## 核心功能

1.  **思维对齐三闸门**：边界嗅探 -> 骨架提案 -> 白箱交付。
2.  **状态闭环**：自动关联 AICloud Lite 的 `cowork/state.md`，只以当前状态作为决策依据；状态变更只能通过 `cowork/patch.json` 表达。
3.  **工程四项红线**：编码前思考、至简至上、精准手术、目标驱动。

## 如何使用

该技能设计为自动激活。只需像往常一样提出需求，AI 将引导你进入思维对齐流程。
