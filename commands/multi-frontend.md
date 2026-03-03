---
title: /multi-frontend Command
description: Frontend-focused development workflow with Gemini leading
---

# /multi-frontend Command

Frontend-focused workflow (Research → Ideation → Plan → Execute → Optimize → Review), Gemini-led.

## Command Syntax

```bash
/multi-frontend <UI task description>
```

<ParamField path="UI task description" type="string" required>
  Description of the frontend task (component design, responsive layout, UI animations, style optimization)
</ParamField>

## Collaborative Models

- **Gemini** - Frontend UI/UX (**Frontend authority, trustworthy**)
- **Codex** - Backend perspective (**Frontend opinions for reference only**)
- **Claude (self)** - Orchestration, planning, execution, delivery

## Core Workflow

### Phase 0: Prompt Enhancement (Optional)

`[Mode: Prepare]` - If ace-tool MCP available, call `mcp__ace-tool__enhance_prompt`

### Phase 1: Research

`[Mode: Research]` - Understand requirements and gather context

1. **Code Retrieval** (if ace-tool MCP available): Call `mcp__ace-tool__search_context`
2. Requirement completeness score (0-10): ≥7 continue, &lt;7 stop and supplement

### Phase 2: Ideation

`[Mode: Ideation]` - Gemini-led analysis

**MUST call Gemini**:
- ROLE_FILE: `~/.claude/.ccg/prompts/gemini/analyzer.md`
- OUTPUT: UI feasibility analysis, recommended solutions (at least 2), UX evaluation

**Save SESSION_ID** (`GEMINI_SESSION`) for subsequent phase reuse.

Output solutions (at least 2), wait for user selection.

### Phase 3: Planning

`[Mode: Plan]` - Gemini-led planning

**MUST call Gemini** (use `resume <GEMINI_SESSION>`):
- ROLE_FILE: `~/.claude/.ccg/prompts/gemini/architect.md`
- OUTPUT: Component structure, UI flow, styling approach

Claude synthesizes plan, save to `.claude/plan/task-name.md` after user approval.

### Phase 4: Implementation

`[Mode: Execute]` - Code development

- Strictly follow approved plan
- Follow existing project design system and code standards
- Ensure responsiveness, accessibility

### Phase 5: Optimization

`[Mode: Optimize]` - Gemini-led review

**MUST call Gemini**:
- ROLE_FILE: `~/.claude/.ccg/prompts/gemini/reviewer.md`
- OUTPUT: Accessibility, responsiveness, performance, design consistency issues list

Integrate review feedback, execute optimization after user confirmation.

### Phase 6: Quality Review

`[Mode: Review]` - Final evaluation

- Check completion against plan
- Verify responsiveness and accessibility
- Report issues and recommendations

## Communication Guidelines

1. Start responses with mode label `[Mode: X]`, initial is `[Mode: Research]`
2. Follow strict sequence: `Research → Ideation → Plan → Execute → Optimize → Review`
3. Use `AskUserQuestion` tool for user interaction

## Key Rules

1. **Gemini frontend opinions are trustworthy**
2. **Codex frontend opinions for reference only**
3. External models have **zero filesystem write access**
4. Claude handles all code writes and file operations

## Examples

```bash
/multi-frontend Design and implement responsive market card component with animations
```

## Related

- **Commands**: `/multi-workflow`, `/multi-backend`, `/multi-plan`
