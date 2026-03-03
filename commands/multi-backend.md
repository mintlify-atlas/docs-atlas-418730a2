---
title: /multi-backend Command
description: Backend-focused development workflow with Codex leading
---

# /multi-backend Command

Backend-focused workflow (Research → Ideation → Plan → Execute → Optimize → Review), Codex-led.

## Command Syntax

```bash
/multi-backend <backend task description>
```

<ParamField path="backend task description" type="string" required>
  Description of the backend task (API design, algorithms, database, business logic)
</ParamField>

## Collaborative Models

- **Codex** - Backend logic, algorithms (**Backend authority, trustworthy**)
- **Gemini** - Frontend perspective (**Backend opinions for reference only**)
- **Claude (self)** - Orchestration, planning, execution, delivery

## Core Workflow

### Phase 0: Prompt Enhancement (Optional)

`[Mode: Prepare]` - If ace-tool MCP available, call `mcp__ace-tool__enhance_prompt`

### Phase 1: Research

`[Mode: Research]` - Understand requirements and gather context

1. **Code Retrieval** (if ace-tool MCP available): Call `mcp__ace-tool__search_context`
2. Requirement completeness score (0-10): ≥7 continue, &lt;7 stop and supplement

### Phase 2: Ideation

`[Mode: Ideation]` - Codex-led analysis

**MUST call Codex**:
- ROLE_FILE: `~/.claude/.ccg/prompts/codex/analyzer.md`
- OUTPUT: Technical feasibility analysis, recommended solutions (at least 2), risk assessment

**Save SESSION_ID** (`CODEX_SESSION`) for subsequent phase reuse.

Output solutions (at least 2), wait for user selection.

### Phase 3: Planning

`[Mode: Plan]` - Codex-led planning

**MUST call Codex** (use `resume <CODEX_SESSION>`):
- ROLE_FILE: `~/.claude/.ccg/prompts/codex/architect.md`
- OUTPUT: File structure, function/class design, dependency relationships

Claude synthesizes plan, save to `.claude/plan/task-name.md` after user approval.

### Phase 4: Implementation

`[Mode: Execute]` - Code development

- Strictly follow approved plan
- Follow existing project code standards
- Ensure error handling, security, performance optimization

### Phase 5: Optimization

`[Mode: Optimize]` - Codex-led review

**MUST call Codex**:
- ROLE_FILE: `~/.claude/.ccg/prompts/codex/reviewer.md`
- OUTPUT: Security, performance, error handling, API compliance issues list

Integrate review feedback, execute optimization after user confirmation.

### Phase 6: Quality Review

`[Mode: Review]` - Final evaluation

- Check completion against plan
- Run tests to verify functionality
- Report issues and recommendations

## Communication Guidelines

1. Start responses with mode label `[Mode: X]`, initial is `[Mode: Research]`
2. Follow strict sequence: `Research → Ideation → Plan → Execute → Optimize → Review`
3. Use `AskUserQuestion` tool for user interaction

## Key Rules

1. **Codex backend opinions are trustworthy**
2. **Gemini backend opinions for reference only**
3. External models have **zero filesystem write access**
4. Claude handles all code writes and file operations

## Examples

```bash
/multi-backend Design and implement user authentication API with JWT
```

## Related

- **Commands**: `/multi-workflow`, `/multi-frontend`, `/multi-plan`
