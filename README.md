# AI Skills Toolkit

面向 Codex、Claude Code、Gemini 等 AI 编码助手的轻量技能库。目前维护 3 个独立 Skill，分别覆盖多智能体协作、PowerShell 安全调用和高影响工程任务的需求对齐。

## Skills

| Skill | 用途 | 入口 |
| --- | --- | --- |
| `cowork-skill-light` | 使用 `cowork/state.md` 与 `cowork/patch.json` 协调多个 AI agent，保持单一当前状态，不维护日志或历史档案 | [`SKILL.md`](./cowork-skill-light/SKILL.md) |
| `powershell-safe-invocation` | 在 Windows 上安全编写和执行 PowerShell，处理原生命令参数、路径转义、进程启动与文件操作 | [`SKILL.md`](./powershell-safe-invocation/SKILL.md) |
| `think-same-skill` | 在高影响工程任务开始前对齐需求、架构和关键取舍；简单、可逆的任务仍可直接执行 | [`SKILL.md`](./think-same-skill/SKILL.md) |

## 克隆仓库

```powershell
git clone https://github.com/awkervic/skill.git
Set-Location skill
```

## 安装到 Codex

使用 Codex 自带的 Skill Installer，将三个技能安装到用户技能目录：

```powershell
$installer = "$HOME\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py"

python $installer `
  --repo awkervic/skill `
  --path cowork-skill-light powershell-safe-invocation think-same-skill
```

安装完成后重启 Codex，使新 Skill 完整加载。

## 更新

仓库副本可通过以下命令更新：

```powershell
git pull --ff-only
```

如需更新 Codex 中已安装的版本，请先删除对应的用户 Skill 目录，再重新运行上面的安装命令。不要删除 `$HOME\.codex\skills\.system`，该目录包含 Codex 内置技能。

## 目录结构

```text
skill/
├── cowork-skill-light/
│   └── SKILL.md
├── powershell-safe-invocation/
│   ├── SKILL.md
│   └── reference.md
├── think-same-skill/
│   └── SKILL.md
└── README.md
```

每个技能以 `SKILL.md` 作为入口；部分技能还包含面向其他 AI 工具的适配文件或补充参考资料。
