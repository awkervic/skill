# Claude Code Instructions

## 🌌 Neat Awker — Twin-Track Lightweight Memory & Matrix Pruning

This project uses the optimized **Neat Awker** for efficient, lossless memory management without token bloating or lagging.

### ⚙️ Activation
1. **Three-in-One Master Workflow**: When user says **"/neat-awker"** or **"整理对话"**, or when encountering a long conversation history, you MUST enforce the Three-in-One master sequence (includes logic distillation, twin-track memory sync, and physical workspace cleanup).
2. **Workspace Cleanup (Shortcut)**: When user says **"/clean"** or **"清理缓存"**, perform quick workspace physical cleanup only (preserving session cache to prevent token bloat).
3. **Knowledge Distillation (Shortcut)**: When user says **"/distill"** or **"提炼思路"**, perform logic distillation to `LOGIC_BASE.md` and subsequent workspace cleanup.

### 🚨 Deep Linkage with think-same-skill (Enforced Thought Alignment)
1. **No Presumptuous Delivery**: For any request involving coding, system architecture, config logic, or technical design, **you are STRICTLY FORBIDDEN from writing code or designing the final solution directly (to prevent AI hallucination/wild guesses)**. You MUST automatically trigger and enter **【Phase 1: Boundary Sniffing and Inverse Questioning】** of `think-same-skill` first!
2. **Abide by Engineering Red Lines**: You must be fully bounded by the four engineering delivery red lines (Think Before Coding, Simplicity First, Surgical Precision, Goal-Driven Execution) defined in `think-same-skill`.
3. **Rules Alignment**: You must actively read and refer to `ai归档/核心规则/rules.md` maintained by `neat-awker` as the baseline. **Note: Rules and logical paths are dynamically evolving reference systems, not rigid dogmas; they must adapt as the project evolves.**

### 🛠️ Three-in-One Master Workflow Guidelines

Upon receiving `/neat-awker` or `整理对话`, execute the following steps in sequence:

1. **Step 1: Logic Distillation & Knowledge Archive**
   - Review the session, extract user's **specific approaches** and **core design decisions**. Write them to `LOGIC_BASE.md` at workspace root (create if missing). Treat these as highly valuable references that should dynamically evolve with the project.
   - Format: `[Date] | [Task Goal] | [Core Solution] | [Anti-Trap/Logic Reason]`.

2. **Step 2: Twin-Track Backup & Rules Pruning**
   - **Track 1 (Chronicle - Write-Only)**: Append session events snapshot and summaries to `ai归档/编年体记忆/memory.md` & `Summarize.md`. Never read these files back.
   - **Track 2 (Rules - Pruning)**: Read `ai归档/核心规则/rules.md` and update with active APIs/routes/env vars via change matrix. **Purge all expired/completed guidelines**; keep it under 80 lines.

3. **Step 3: Workspace Clean Up (Preserving Session Cache)**
   - **Keep Session Cache Intact**: To protect Local Context Caching and avoid server token bloat, **DO NOT** delete any `Task Logs`, transcripts, or session files under `C:\Users\Dell\.gemini\antigravity-cli\brain\<UUID>`.
   - **Physical Delete**:
     * Remove all intermediate `scratch` python files from the workspace (do not touch `brain` folder).
     * Force delete all generated `__pycache__` folders at the workspace root.
   - **Safety Boundary**: Do NOT touch any user-created `.py`, `.xlsx`, `.csv`, or other data assets.

4. **Reply Template**:
   - Briefly list the saved core logic items.
   - Confirm: *"核心灵魂已锁死在 LOGIC_BASE.md，会话缓存已安全保留以节省 Token 消耗。"*
   - Prompt the user that they are in an ultra-clean environment and can start a brand new, zero-token chat immediately!

---

Please refer to [SKILL.md](./SKILL.md) for the full execution workflow and formatting rules.
