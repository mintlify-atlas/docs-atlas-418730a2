---
title: /skill-create Command
description: Analyze git history to extract coding patterns and generate SKILL.md files
---

# /skill-create Command

Analyze your repository's git history to extract coding patterns and generate SKILL.md files that teach Claude your team's practices.

## Command Syntax

```bash
/skill-create [options]
```

<ParamField path="--commits" type="number" default="200">
  Number of recent commits to analyze
</ParamField>

<ParamField path="--output" type="string">
  Custom output directory for generated skills
</ParamField>

<ParamField path="--instincts" type="boolean">
  Also generate instincts for continuous-learning-v2
</ParamField>

## What It Does

1. **Parses Git History** - Analyzes commits, file changes, and patterns
2. **Detects Patterns** - Identifies recurring workflows and conventions
3. **Generates SKILL.md** - Creates valid Claude Code skill files
4. **Optionally Creates Instincts** - For the continuous-learning-v2 system

## Examples

```bash
# Analyze current repo
/skill-create

# Analyze last 100 commits
/skill-create --commits 100

# Custom output directory
/skill-create --output ./skills

# Also generate instincts
/skill-create --instincts
```

## Pattern Detection

| Pattern | Detection Method |
|---------|------------------|
| **Commit conventions** | Regex on commit messages (feat:, fix:, chore:) |
| **File co-changes** | Files that always change together |
| **Workflow sequences** | Repeated file change patterns |
| **Architecture** | Folder structure and naming conventions |
| **Testing patterns** | Test file locations, naming, coverage |

## Example Output

```markdown
---
name: my-app-patterns
description: Coding patterns from my-app repository
version: 1.0.0
source: local-git-analysis
analyzed_commits: 150
---

# My App Patterns

## Commit Conventions

This project uses **conventional commits**:
- `feat:` - New features
- `fix:` - Bug fixes
- `chore:` - Maintenance tasks
- `docs:` - Documentation updates

## Code Architecture

```
src/
├── components/     # React components (PascalCase.tsx)
├── hooks/          # Custom hooks (use*.ts)
├── utils/          # Utility functions
├── types/          # TypeScript type definitions
└── services/       # API and external services
```

## Workflows

### Adding a New Component
1. Create `src/components/ComponentName.tsx`
2. Add tests in `src/components/__tests__/ComponentName.test.tsx`
3. Export from `src/components/index.ts`

## Testing Patterns

- Test files: `__tests__/` directories or `.test.ts` suffix
- Coverage target: 80%+
- Framework: Vitest
```

## GitHub App Integration

For advanced features (10k+ commits, team sharing, auto-PRs), use the [Skill Creator GitHub App](https://github.com/apps/skill-creator).

## Related

- **Commands**: `/instinct-import`, `/instinct-status`, `/evolve`
