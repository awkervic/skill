---
name: cowork-skill-light
description: AICloud Lite patch-based multi-agent state machine. 任意 agent 只读 cowork/state.md，只输出 cowork/patch.json，由 merge engine 合并并更新 state.md。
---

# AICloud Lite

你是 AICloud Lite 的执行器。

系统采用 patch-based multi-agent state machine。它不是记录系统，而是一个由 `state.md` 和 `patch.json` 驱动的持续压缩状态机。

## 核心规则

1. `cowork/state.md` 是唯一真相源。
2. 所有 agent 只能读取 `cowork/state.md`。
3. 所有 agent 只能输出 `cowork/patch.json`。
4. agent 不允许直接修改 `cowork/state.md`。
5. merge engine 负责读取 patch、合并状态、更新 `cowork/state.md`。
6. 系统必须支持任意 agent，例如 opencode、codex、any LLM。
7. 禁止角色绑定，不得固定 Claude / Codex / Agy 等职责。

## 文件结构

在项目根目录确保存在：

```text
cowork/
├── state.md
└── patch.json
```

缺失时允许初始化。除此之外，不得创建长期记录文件。

禁止创建或依赖：

- `logs/`
- history journal
- neat
- archive
- memory
- distill
- 长期累积文本
- agent 专属长期文件

## state.md 规范

`cowork/state.md` 必须短、小、可读、结构化，并只表达当前状态。

推荐结构：

```markdown
# 当前目标
（当前任务）

# 当前状态
（系统当前事实）

# 当前进度
（已完成内容）

# 决策
（只保留最终结论）

# 待办
（下一步）
```

规则：

- `state.md` 只能由 merge engine 更新。
- agent 禁止直接写入 `state.md`。
- 禁止 append。
- merge engine 必须 overwrite。
- merge engine 必须压缩信息，删除冗余内容。
- merge engine 只保留最终决策，不保留历史版本。

## patch.json 规范

agent 的唯一输出是 `cowork/patch.json`。

`patch.json` 必须是 JSON，建议结构：

```json
{
  "agent": "any-agent-name",
  "task": "本轮任务",
  "observations": [
    "从 state.md 得出的当前事实"
  ],
  "changes": [
    {
      "section": "当前进度",
      "op": "replace",
      "content": "建议写入 state.md 的压缩内容"
    }
  ],
  "decisions": [
    "本轮建议保留的最终决策"
  ],
  "todos": [
    "下一步任务"
  ]
}
```

约束：

- patch 只描述建议变更，不直接改 `state.md`。
- patch 必须短小，不写长篇推理。
- patch 不保存历史。
- patch 不引用 logs、history、archive、neat 或其他长期记录。
- patch 应当能被 merge engine 无歧义合并。

## 固定流程

每轮任务按以下顺序执行：

1. agent 读取 `cowork/state.md`。
2. agent 执行任务。
3. agent 生成 `cowork/patch.json`。
4. merge engine 读取 `cowork/state.md` 与 `cowork/patch.json`。
5. merge engine 合并 patch。
6. merge engine overwrite 更新 `cowork/state.md`。
7. 下一轮 agent 继续只读新的 `cowork/state.md`。

## merge engine 合并规则

merge engine 必须：

1. 只信任 `state.md` 当前内容和本轮 `patch.json`。
2. 删除重复信息。
3. 合并相似内容。
4. 保留最终决策。
5. 删除中间过程和历史版本。
6. 保持 `state.md` 短、小、可读。
7. overwrite `state.md`，禁止 append。

## Agent 行为规则

任意 agent 都遵守同一协议：

- 只能读取 `cowork/state.md`。
- 只能输出 `cowork/patch.json`。
- 不得写入 `cowork/state.md`。
- 不得读取或生成长期历史文件。
- 不得假设自己拥有固定角色。
- 需要研究、编码、规划或审查时，都通过 patch 表达结果。

## 启动任务模板

当用户要求启动 AICloud Lite 或 cowork-skill-light 时：

1. 若 `cowork/state.md` 缺失，创建推荐结构的空状态。
2. 若 `cowork/patch.json` 缺失，创建空 patch 或等待 agent 输出。
3. agent 读取 `state.md`。
4. agent 基于用户任务生成 `patch.json`。
5. merge engine 合并 patch 并 overwrite `state.md`。

## 禁止事项

- 禁止 logs
- 禁止 history
- 禁止 neat
- 禁止长期记录文件
- 禁止角色绑定
- 禁止 agent 直接修改 `state.md`
- 禁止 agent 输出 `patch.json` 以外的长期协作文件
