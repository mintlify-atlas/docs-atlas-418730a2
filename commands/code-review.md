---
title: /code-review Command
description: Comprehensive security and quality review of uncommitted changes
---

# /code-review Command

Comprehensive security and quality review of uncommitted changes before committing.

## What This Command Does

1. Get changed files: `git diff --name-only HEAD`
2. Check each file for security issues, code quality, and best practices
3. Generate report with severity levels and suggested fixes
4. Block commit if CRITICAL or HIGH issues found

## Review Categories

### Security Issues (CRITICAL)

- Hardcoded credentials, API keys, tokens
- SQL injection vulnerabilities
- XSS vulnerabilities
- Missing input validation
- Insecure dependencies
- Path traversal risks

### Code Quality (HIGH)

- Functions > 50 lines
- Files > 800 lines
- Nesting depth > 4 levels
- Missing error handling
- console.log statements
- TODO/FIXME comments
- Missing JSDoc for public APIs

### Best Practices (MEDIUM)

- Mutation patterns (use immutable instead)
- Emoji usage in code/comments
- Missing tests for new code
- Accessibility issues (a11y)

## Command Syntax

```bash
/code-review
```

No arguments required - automatically reviews all uncommitted changes.

## Example Output

```markdown
# Code Review Report

## Files Changed
- src/auth.ts (modified)
- src/api/users.ts (modified)

## Issues Found

[CRITICAL] Hardcoded API Key
File: src/auth.ts:15
Issue: API key hardcoded in source
Suggestion: Move to environment variable

Before:
```typescript
const apiKey = "sk_live_abc123xyz";
```

After:
```typescript
const apiKey = process.env.API_KEY;
if (!apiKey) throw new Error("API_KEY required");
```

[HIGH] Missing Error Handling
File: src/api/users.ts:42
Issue: Network call without try/catch
Suggestion: Wrap in try/catch

Before:
```typescript
const user = await fetchUser(id);
```

After:
```typescript
try {
  const user = await fetchUser(id);
} catch (error) {
  logger.error("Failed to fetch user", { id, error });
  throw new Error("User fetch failed");
}
```

## Summary
- CRITICAL: 1
- HIGH: 1
- MEDIUM: 0

Recommendation: ❌ Block commit until CRITICAL issue is fixed
```

## Approval Criteria

| Status | Condition |
|--------|----------|
| ✅ Approve | No CRITICAL or HIGH issues |
| ⚠️ Warning | Only MEDIUM issues (merge with caution) |
| ❌ Block | CRITICAL or HIGH issues found |

## Important Notes

<Warning>
  Never approve code with security vulnerabilities! Always fix CRITICAL issues before committing.
</Warning>

## Integration with Other Commands

- Use after writing/modifying code
- Use before committing changes
- Combine with `/verify` for full checks

## Related

- **Agent**: `agents/code-reviewer.md`
- **Commands**: `/verify`, `/security`, `/go-review`, `/python-review`
