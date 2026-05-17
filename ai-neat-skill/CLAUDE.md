# Claude Code Instructions

This file provides project-specific instructions for Claude Code.

## 🌌 AI Neat Skill (Chronicle Memory Pruning)

This project uses the **AI Neat Skill** for efficient, lossless memory management.

### ⚙️ Activation
When you encounter long conversation history or the user says **"编年史"**, **"/ai-neat-skill"**, or **"整理记忆"**, you MUST follow the protocol defined in [SKILL.md](./SKILL.md).

### 📋 Core Responsibilities
1.  **Do Not Erase History Blindly**: Never discard context without first extracting key events.
2.  **Extract Chronicles**: Summarize debugging/development sessions into atomic, date-stamped snapshots.
3.  **Sync to memory.md**: Append these snapshots to `memory.md` following the specified format.
4.  **Handover**: Before pruning context, record [PENDING] tasks at the end of `memory.md`.

Please refer to [SKILL.md](./SKILL.md) for the full execution workflow and formatting rules.
