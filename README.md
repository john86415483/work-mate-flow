# work-mate-flow

AI 编码 Agent 的 Skills 和工作流插件，支持 Claude Code 和 OpenCode。

## 安装

### Claude Code

作为插件安装：

```bash
/plugin install work-mate-flow@git+https://github.com/john/work-mate-flow.git
```

### OpenCode

让 OpenCode 读取安装指引并自动完成安装：

```
Fetch and follow instructions from https://raw.githubusercontent.com/john86415483/work-mate-flow/refs/heads/main/.opencode/INSTALL.md
```

## 添加 Skill

每个 skill 是一个放在 `skills/` 下的目录，内含带 YAML frontmatter 的 `SKILL.md` 文件：

```markdown
---
name: my-skill
description: Use when [条件] - [作用]
---

# My Skill

[内容]
```

Agent 通过 `using-workmateflow` 引导机制自动加载 skill。