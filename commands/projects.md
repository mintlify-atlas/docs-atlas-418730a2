---
title: /projects Command
description: List known projects and their instinct statistics
---

# /projects Command

List project registry entries and per-project instinct/observation counts.

## Command Syntax

```bash
/projects
```

No arguments required.

## What It Shows

For each project:
- Project name, ID, root, remote
- Personal and inherited instinct counts
- Observation event count
- Last seen timestamp

Also displays global instinct totals.

## Example Output

```
📊 Projects
===========

## my-app
ID: a1b2c3d4e5f6
Root: /Users/me/projects/my-app
Remote: github.com/me/my-app
Instincts: 8 personal, 3 inherited
Observations: 142
Last seen: 2026-03-03 14:30

## other-project
ID: 9f8e7d6c5b4a
Root: /Users/me/projects/other
Remote: github.com/me/other
Instincts: 5 personal, 1 inherited
Observations: 67
Last seen: 2026-03-01 09:15

---
Global instincts: 12
```

## Related

- **Commands**: `/instinct-status`, `/promote`
- **Skill**: `skills/continuous-learning-v2/`
