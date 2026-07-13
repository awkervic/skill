---
name: think-same-skill
description: Align requirements and architecture before high-impact engineering work. Use when the user invokes /align or asks for staged design approval, or when unresolved choices would materially change architecture, safety, cost, compatibility, or scope. Do not force alignment gates for small, reversible, well-specified changes.
---

# 思维对齐与工程交付

根据任务风险选择流程强度。简单、可逆、边界清晰的任务直接执行并验证；只有关键选择会显著改变结果时才进入确认闸门。

## 对齐闸门

### 第一阶段：边界与关键选择

1. 用一句话复述目标和成功标准。
2. 指出会改变方案的未知项及主要风险。
3. 仅提出无法从项目中发现、且不宜安全假设的 1–3 个关键问题。
4. 等待确认；不要在此阶段输出完整实现。

不要为了流程而提问。能通过只读检查发现的信息先自行检查；可安全回退的细节采用合理默认值并明确说明。

### 第二阶段：方案骨架

1. 给出核心技术选择及理由。
2. 展示最小模块、数据流或目录结构。
3. 列出验证方式和关键取舍。
4. 当用户要求分阶段批准时等待确认，否则在已授权实施的任务中继续执行。

### 第三阶段：白箱交付

1. 只修改实现目标所需的内容。
2. 保持代码和说明可扫描、可追溯。
3. 验证成功标准，并报告实际结果与剩余限制。

## 工程红线

- 不隐藏不确定性，不伪造验证结果。
- 不进行与需求无关的重构、格式化或清理。
- 匹配现有架构和风格，优先采用最小可维护实现。
- 只清理由本次修改直接产生的孤儿代码或依赖。
- 对 Bug 修复优先建立可复现证据；对重构确认行为保持一致。
- 多步骤任务使用精简计划，每一步都配有可执行验证。

## 与 AICloud Lite 协作

仅当项目明确启用 `cowork-skill-light` 时：

1. 读取 `cowork/state.md` 的当前目标、状态、决策和待办。
2. 通过 `cowork/patch.json` 提议状态变更。
3. 不直接修改 `state.md`，不创建历史或 agent 专属记录。

未启用 AICloud Lite 时，不要求创建 `cowork/` 文件。
