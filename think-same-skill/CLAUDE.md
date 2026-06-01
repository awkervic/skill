# Claude Code Instructions

This file provides project-specific instructions for Claude Code.

## ⚙️ think-same-skill (Thought Alignment & Engineering Protocol)

This project uses the **think-same-skill** to ensure deep alignment between the user and the AI, and to maintain high engineering standards.

### ⚙️ Activation
- **Mandatory Auto-Trigger**: For any coding, system architecture, config logic, function implementation, code refactoring, or modification request, **you are STRICTLY PROHIBITED from designing solutions or writing code directly**. You MUST automatically trigger and enter **【Phase 1: Boundary Sniffing and Inverse Questioning】** of this skill to align thoughts with the user!
- **Keyword Triggers**: Active on `/align`, `思维对齐`, `开始对齐`, `方案设计`, or `开发任务`.
- **Memory & Rules Sync**: You must synchronize and read `ai归档/核心规则/rules.md` maintained by `neat-awker` first to ensure full alignment with historical boundaries and rules.
- **Three-Gate Phase**: You MUST follow the "Boundary Sniffing", "Skeleton Proposal", and "White-box Delivery" stages sequentially.

### 📋 Core Responsibilities & Engineering Red Lines
1. **Think Before Coding**: Declaration of boundaries,分支暴露, explicit questions upon confusion. Stop and ask!
2. **Simplicity First**: Write the absolute minimum code required; refuse single-use abstractions and premature over-engineering.
3. **Surgical Precision**: Keep changes precise; only modify what is necessary; preserve unrelated code intact.
4. **Goal Driven**: Quantitative success criteria and step-by-step verification plan before executing multi-step tasks.

Refer to [SKILL.md](./SKILL.md) for the full protocol details.
