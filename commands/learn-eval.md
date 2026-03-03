---
title: /learn-eval Command
description: Extract, evaluate, and save reusable patterns with quality gate
---

# /learn-eval Command

Extends `/learn` with a quality gate and save-location decision before writing any skill file.

## Process

1. Review session for extractable patterns
2. Identify the most valuable/reusable insight
3. **Determine save location:**
   - **Global** (`~/.claude/skills/learned/`): Generic patterns usable across 2+ projects
   - **Project** (`.claude/skills/learned/`): Project-specific knowledge
4. Draft the skill file
5. **Self-evaluate** using quality rubric
6. Ask user to confirm with scores table
7. Save to determined location

## Quality Rubric

| Dimension | 1 | 3 | 5 |
|-----------|---|---|---|
| **Specificity** | Abstract principles only | Representative example present | Rich examples covering all patterns |
| **Actionability** | Unclear what to do | Main steps understandable | Immediately actionable, edge cases covered |
| **Scope Fit** | Too broad or too narrow | Mostly appropriate | Name, trigger, and content perfectly aligned |
| **Non-redundancy** | Nearly identical to another skill | Some overlap but unique | Completely unique value |
| **Coverage** | Covers fraction of task | Main cases covered | Main cases, edge cases, and pitfalls covered |

## Command Syntax

```bash
/learn-eval
```

No arguments required - analyzes current session.

## Evaluation Output

```markdown
| Dimension | Score | Rationale |
|-----------|-------|-----------|  
| Specificity | 4/5 | Has code examples for main use cases |
| Actionability | 5/5 | Step-by-step instructions with commands |
| Scope Fit | 4/5 | Slightly broader than name suggests |
| Non-redundancy | 5/5 | Unique pattern not in existing skills |
| Coverage | 4/5 | Main cases covered, missing error handling |
| **Total** | **22/25** | |

**Save Location**: Global (~/.claude/skills/learned/)
**Filename**: async-error-handling.md

Proceed with save? (yes/no)
```

## Requirements

- All dimensions must score ≥ 3 before saving
- If any dimension scores 1-2, improve draft and re-score
- User must explicitly confirm before writing

## Related

- **Commands**: `/learn`, `/skill-create`, `/evolve`
