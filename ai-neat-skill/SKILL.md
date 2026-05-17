---
name: ai-neat-skill
description: AI 编年史记忆剪枝技能。用于提炼核心事件快照、压缩上下文、同步 memory.md 记忆文件。当上下文接近限制或对话过长时触发。
---

# 🌌 AI Neat Skill — AI 编年史记忆剪枝技能

## 📋 技能定义 (Skill Definition)

### 🎯 激活触发器 (Activation Triggers)
当满足以下任一条件时，必须启动该技能：
1. 用户输入关键字：`“编年史”`、`“/ai-neat-skill”`、`“整理记忆”`。
2. 上下文长度接近 Token 限制 (80%+) 或 连续对话超过 20 轮。
3. 项目初始化或关键阶段结束，需要进行状态同步。

### ⚙️ 核心协议 (Core Protocol)
1. **禁止直接抹除**：严禁在未备份核心事件的情况下直接丢弃历史上下文。
2. **编年史压缩**：将琐碎的调试过程提炼为 [精确日期] 驱动的「核心事件快照」。
3. **原子化存储**：每个独立事件在 `memory.md` 中占用且仅占用一行。

### 🛠️ 执行流程 (Workflow)

#### 第零步：尺寸体检 (Pre-flight Check)
- 检查 `memory.md`：若超过 200 行，执行二次压缩。
- 去重：比对现有快照，防止重复记录相同事件。

#### 第一步：事件盘点 (Inventory)
识别以下高价值信息：
- **架构/设计决策** (Architecture/Design)
- **功能增量** (Feature Increment)
- **关键 Bug 修复** (Critical Fixes)
- **环境变更** (Environment Changes)

#### 第二步：提取快照 (Extraction)
- **格式规范**：`[YYYY-MM-DD] <分类>：<事件描述> (指针/关联路径)`
- **绝对日期**：使用 `2026-05-17` 格式。
- **深层链接**：关联到具体的文档或代码段（例如：`详见 README.md`）。

#### 第三步：同步与交接 (Sync & Handover)
1. **记忆同步**：
   - 将新快照追加在 `memory.md` 的 `---` 分割线之后。
   - **减优于加**：更新或合并冗余的旧快照。
2. **上下文交接 (Context Handover)**：
   - 识别当前 **[PENDING]** 任务，在 `memory.md` 末尾记录“下一步计划”。

#### 第四步：自检 (Validation)
- [ ] 所有快照包含精确日期？
- [ ] 保持单行格式？
- [ ] 写入确认？

## 📂 资源引用 (References)
- **memory.md**：项目编年史记忆文件。
