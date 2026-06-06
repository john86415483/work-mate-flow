# work-mate-flow

AI coding agent skills and workflows for Claude Code and OpenCode.

## Installation

### Claude Code

Add as a plugin:

```bash
/plugin install work-mate-flow@git+https://github.com/john/work-mate-flow.git
```

### OpenCode

Add to `opencode.json`:

```json
{
  "plugin": ["work-mate-flow@git+https://github.com/john/work-mate-flow.git"]
}
```

## Adding Skills

Each skill is a directory under `skills/` containing a `SKILL.md` file with YAML frontmatter:

```markdown
---
name: my-skill
description: Use when [condition] - [what it does]
---

# My Skill

[Content here]
```

The agent loads skills automatically via the `using-workmateflow` bootstrap mechanism.
