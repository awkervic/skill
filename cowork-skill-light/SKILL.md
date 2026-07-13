---
name: cowork-skill-light
description: Coordinate multiple AI agents through an AICloud Lite patch-based state machine. Use when a project explicitly adopts cowork/state.md as the single current-state source and requires agents to propose changes through cowork/patch.json without maintaining logs, histories, role-bound files, or other long-term records.
---

# AICloud Lite

Maintain a compact current-state machine. Do not turn it into a history or logging system.

## Invariants

1. Treat `cowork/state.md` as the only source of current truth.
2. Let agents read `state.md` and write only proposals to `cowork/patch.json`.
3. Do not let agents modify `state.md` directly.
4. Let the merge engine combine the patch and overwrite `state.md`.
5. Keep the protocol agent-neutral; do not bind responsibilities to Claude, Codex, Gemini, or another named model.
6. Do not create or depend on logs, journals, archives, memory, distillation files, or agent-specific long-term files.

## Required files

```text
cowork/
├── state.md
└── patch.json
```

Initialize missing files only when the user starts this protocol.

Use this compact state structure:

```markdown
# 当前目标

# 当前状态

# 当前进度

# 决策

# 待办
```

Keep only current facts, completed outcomes, final decisions, and next actions. Remove obsolete alternatives and intermediate reasoning. Always overwrite; never append history.

## Patch format

```json
{
  "agent": "agent-name",
  "task": "current task",
  "observations": ["current fact"],
  "changes": [
    {
      "section": "当前进度",
      "op": "replace",
      "content": "compressed proposed state"
    }
  ],
  "decisions": ["final decision"],
  "todos": ["next action"]
}
```

Produce valid JSON. Keep proposals short and unambiguous. Do not include chain-of-thought, historical narratives, or references to forbidden files.

## Merge cycle

1. Read the current `state.md`.
2. Perform the assigned task.
3. Write a proposed `patch.json`.
4. Have the merge engine validate the patch against the current state.
5. Deduplicate and compress proposed changes.
6. Preserve final decisions and current todos.
7. Atomically overwrite `state.md`.

Reject malformed patches, unknown sections, unsupported operations, or changes based on stale state. When concurrent patches conflict, require the merge engine to resolve them explicitly rather than silently choosing one.
