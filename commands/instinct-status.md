---
title: /instinct-status Command
description: Show learned instincts grouped by domain with confidence levels
---

# /instinct-status Command

Shows learned instincts for the current project plus global instincts, grouped by domain.

## What It Shows

1. Detects current project context (git remote/path hash)
2. Reads project instincts from `~/.claude/homunculus/projects/<project-id>/instincts/`
3. Reads global instincts from `~/.claude/homunculus/instincts/`
4. Merges with precedence (project overrides global when IDs collide)
5. Displays grouped by domain with confidence bars

## Command Syntax

```bash
/instinct-status
```

No arguments required.

## Example Output

```
============================================================
  INSTINCT STATUS - 12 total
============================================================

  Project: my-app (a1b2c3d4e5f6)
  Project instincts: 8
  Global instincts:  4

## PROJECT-SCOPED (my-app)
  ### WORKFLOW (3)
    ███████░░░  70%  grep-before-edit [project]
              trigger: when modifying code

## GLOBAL (apply to all projects)
  ### SECURITY (2)
    █████████░  85%  validate-user-input [global]
              trigger: when handling user input
```

## Related

- **Commands**: `/instinct-export`, `/instinct-import`, `/promote`, `/evolve`
- **Skill**: `skills/continuous-learning-v2/`
