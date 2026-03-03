---
title: /learn Command
description: Extract reusable patterns from the current session
---

# /learn Command

Analyze the current session and extract patterns worth saving as skills.

## When to Use

Run `/learn` at any point during a session when you've solved a non-trivial problem.

## What to Extract

Look for:

1. **Error Resolution Patterns**
   - What error occurred?
   - What was the root cause?
   - What fixed it?
   - Is this reusable for similar errors?

2. **Debugging Techniques**
   - Non-obvious debugging steps
   - Tool combinations that worked
   - Diagnostic patterns

3. **Workarounds**
   - Library quirks
   - API limitations
   - Version-specific fixes

4. **Project-Specific Patterns**
   - Codebase conventions discovered
   - Architecture decisions made
   - Integration patterns

## Command Syntax

```bash
/learn
```

No arguments required - analyzes current session automatically.

## Process

1. Review the session for extractable patterns
2. Identify the most valuable/reusable insight
3. Draft the skill file
4. Ask user to confirm before saving
5. Save to `~/.claude/skills/learned/`

## Output Format

Creates a skill file at `~/.claude/skills/learned/[pattern-name].md`:

```markdown
# [Descriptive Pattern Name]

**Extracted:** 2026-03-03
**Context:** Brief description of when this applies

## Problem
What problem this solves - be specific

## Solution
The pattern/technique/workaround

## Example
```typescript
// Code example
```

## When to Use
Trigger conditions - what should activate this skill
```

## Notes

- Don't extract trivial fixes (typos, simple syntax errors)
- Don't extract one-time issues (specific API outages)
- Focus on patterns that will save time in future sessions
- Keep skills focused - one pattern per skill

## Related

- **Commands**: `/learn-eval`, `/skill-create`, `/evolve`
