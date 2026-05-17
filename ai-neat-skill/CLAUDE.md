# Claude Code Instructions

This file provides project-specific instructions for Claude Code.

## 🌌 AI Neat Skill (Chronicle Memory Pruning)

This project uses the **AI Neat Skill** for efficient, lossless memory management.

### ⚙️ Activation
When you encounter long conversation history or the user says **"编年史"**, **"/ai-neat-skill"**, **"整理记忆"**, or **"同步到根目录"**, you MUST follow the protocol defined in [SKILL.md](./SKILL.md).

### 📋 Core Responsibilities
1.  **Portability First**: Maintain `memory.md` and `Summarize.md` in the project root to ensure memory travels with the code.
2.  **Incremental Summary**: Append changes to `Summarize.md` with Beijing Time `[YYYY-MM-DD HH:mm]`.
3.  **Sync to Root**: Extract snapshots and append them to `<root>/memory.md`.
4.  **No Internal Redundancy**: Do not store memory files inside the skill directory.

Please refer to [SKILL.md](./SKILL.md) for the full execution workflow and formatting rules.
