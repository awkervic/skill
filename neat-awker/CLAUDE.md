# Claude Code Instructions

## 🌌 Neat Awker — Twin-Track Lightweight Memory & Matrix Pruning

This project uses the optimized **Neat Awker** for efficient, lossless memory management without token bloating or lagging.

### ⚙️ Activation
When encountering a long conversation history or when the user says **"编年史"**, **"/neat-awker"**, **"整理记忆"**, **"收尾"**, or **"整理文档"**, you MUST follow the twin-track protocol defined in [SKILL.md](./SKILL.md).

### 📋 Core Responsibilities (Twin-Track Protocol)

1.  **Track 1: Chronicle Archive (Write-Only)**
    *   **Purpose**: Log historical events and incremental changes.
    *   **Path**: `ai归档/编年体记忆/memory.md` and `Summarize.md`.
    *   **Action**: **Do NOT read** the historical contents of these files during operations to save time and tokens. Directly append the new session milestone snapshot (using Beijing Time `[YYYY-MM-DD HH:mm]`). **Never** read or load this file back into active context for reasoning.

2.  **Track 2: Matrix Pruning & Active Rules (Active Guidance)**
    *   **Purpose**: Rules, constraints, cheatsheets, and change matrices that guide the AI's actual coding work.
    *   **Path**: `ai归档/核心规则/rules.md`.
    *   **Action**: Active read & pruning. Reconcile changes (DB tables, API routes, env vars) against rules using the change matrix. Crucially, **purge and delete** all stale, completed, or redundant guidelines. Keep the rules file **strictly under 80 lines**.

3.  **Lightweight Execution (Speed-First)**:
    *   Perform a quick delta inventory of only the *current* session changes, rather than a full deep chat log analysis.
    *   Clean up by moving all temporary drafts, scratch files, and intermediate outputs to the `<root>/ai归档/` directory.

4.  **Automatic Migration & Backward Compatibility (Migration - Auto-run)**:
    *   At the start of pruning, scan and rename any remnant `ai-neat-skill` directories, skill bundles, and old in-file references to `neat-awker` automatically; ignore if already migrated.
    *   Smoothly extract historical redlines/rules from old memories into the new Track 2 `rules.md` on the first run.

Please refer to [SKILL.md](./SKILL.md) for the full execution workflow and formatting rules.
