---
title: /multi-workflow Command
description: Full multi-model workflow from Research to Review with quality gates
---

# /multi-workflow Command

Multi-model collaborative development workflow (Research → Ideation → Plan → Execute → Optimize → Review), with intelligent routing: Frontend → Gemini, Backend → Codex.

## Command Syntax

```bash
/multi-workflow <task description>
```

<ParamField path="task description" type="string" required>
  Description of the task to develop
</ParamField>

## Collaborative Models

- **ace-tool MCP** - Code retrieval + Prompt enhancement
- **Codex** - Backend logic, algorithms, debugging (**Backend authority**)
- **Gemini** - Frontend UI/UX, visual design (**Frontend expert**)
- **Claude (self)** - Orchestration, planning, execution, delivery

## Execution Workflow

### Phase 1: Research & Analysis

`[Mode: Research]` - Understand requirements and gather context:

1. **Prompt Enhancement**: Call `mcp__ace-tool__enhance_prompt`
2. **Context Retrieval**: Call `mcp__ace-tool__search_context`
3. **Requirement Completeness Score** (0-10):
   - ≥7: Continue
   - &lt;7: Stop, ask clarifying questions

### Phase 2: Solution Ideation

`[Mode: Ideation]` - Multi-model parallel analysis:

**Parallel Calls** (`run_in_background: true`):
- Codex: Technical feasibility, solutions, risks
- Gemini: UI feasibility, solutions, UX evaluation

**Save SESSION_ID** (`CODEX_SESSION` and `GEMINI_SESSION`)

Synthesize both analyses, output solution comparison (at least 2 options), wait for user selection.

### Phase 3: Detailed Planning

`[Mode: Plan]` - Multi-model collaborative planning:

**Parallel Calls** (resume session with `resume <SESSION_ID>`):
- Codex: Backend architecture
- Gemini: Frontend architecture

**Claude Synthesis**: Adopt Codex backend plan + Gemini frontend plan, save to `.claude/plan/task-name.md` after user approval.

### Phase 4: Implementation

`[Mode: Execute]` - Code development:

- Strictly follow approved plan
- Follow existing project code standards
- Request feedback at key milestones

### Phase 5: Code Optimization

`[Mode: Optimize]` - Multi-model parallel review:

**Parallel Calls**:
- Codex: Security, performance, error handling
- Gemini: Accessibility, design consistency

Integrate review feedback, execute optimization after user confirmation.

### Phase 6: Quality Review

`[Mode: Review]` - Final evaluation:

- Check completion against plan
- Run tests to verify functionality
- Report issues and recommendations
- Request final user confirmation

## Communication Guidelines

1. Start responses with mode label `[Mode: X]`, initial is `[Mode: Research]`
2. Follow strict sequence: `Research → Ideation → Plan → Execute → Optimize → Review`
3. Request user confirmation after each phase completion
4. Force stop when score < 7 or user does not approve
5. Use `AskUserQuestion` tool for user interaction

## Examples

```bash
/multi-workflow Add user authentication with JWT tokens
```

## Key Rules

1. Phase sequence cannot be skipped (unless user explicitly instructs)
2. External models have **zero filesystem write access**
3. **Force stop** when score < 7 or user does not approve

## Related

- **Commands**: `/multi-plan`, `/multi-execute`, `/multi-backend`, `/multi-frontend`
