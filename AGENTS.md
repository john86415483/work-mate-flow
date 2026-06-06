# work-mate-flow — AI Agent Skills 插件

Skills 插件，支持 Claude Code 和 OpenCode。Skill 存放在 `skills/<name>/SKILL.md`，包含 YAML frontmatter（`name`、`description`）。`using-workmateflow` 引导 skill 在会话启动时自动加载，教会 agent 在采取任何行动前先检查适用的 skill。

## 架构

- `skills/using-workmateflow/SKILL.md` — 引导 skill（自动加载）；agent 必须先检查是否有适用 skill 再行动
- `CLAUDE.md` — `@include` 引导 skill；Claude Code 自动从 `skills/` 发现所有 skill
- `.opencode/plugins/work-mate-flow.js` — OpenCode 插件：通过 `experimental.chat.messages.transform` hook 注入引导 + 通过 `config` hook 注册 skills 目录
- `.claude-plugin/plugin.json` — Claude Code 插件元数据
- `package.json` — npm 入口（`main` → `.opencode/plugins/work-mate-flow.js`）

## 添加 Skill

```markdown
---
name: my-skill
description: Use when [场景] - [作用]
---

# My Skill

[中文内容]
```

每个 skill 一个目录：`skills/<name>/SKILL.md`，不需要其他文件。

## 版本管理

两个文件同步版本号：

| 文件 | 字段 |
|---|---|
| `package.json` | `version` |
| `.claude-plugin/plugin.json` | `version` |

```bash
# 查看当前版本（检测不一致）
bash scripts/bump-version.sh --check

# 升级版本号（自动更新声明文件 + 审计遗漏引用）
bash scripts/bump-version.sh 0.0.2

# 完整审计（扫描仓库中未声明但包含旧版本号的文件）
bash scripts/bump-version.sh --audit
```

## 提交要求

提交前必须先询问用户是否需要升级版本号：
- 版本号每次最后一位数字加 1（patch 升级）
- 如果用户同意，先执行 `bash scripts/bump-version.sh <新版本号>`，再提交
- 如果用户不同意，直接提交不升版本

用户说"提交"时，执行升级版本号 + commit + push 到远端。

```bash
# 示例：当前 0.0.1，升级到 0.0.2
bash scripts/bump-version.sh 0.0.2
git add -A && git commit -m "Bump version to 0.0.2"
```

如需将新文件纳入版本管理，编辑 `.version-bump.json` 的 `files` 数组。

## 平台加载

- **Claude Code**：读取 `CLAUDE.md` → `@include` 加载 `using-workmateflow` → agent 通过 `Skill` 工具调用其他 skill
- **OpenCode**：插件 hooks 在第一条用户消息前注入引导 + 注册 `skills/` 路径 → agent 使用原生 `skill` 工具

Skill 内容语言：中文（项目约定）。
