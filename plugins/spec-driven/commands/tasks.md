---
description: Generate task list from technical plan
argument-hint: [ID]
---

# Tasks Command

Transform the technical plan into an organized, trackable task list.

## Arguments

- `[ID]` - Feature ID (optional if branch is associated)

Arguments received: $ARGUMENTS

## Process

### Step 1: Resolve Feature

If ID provided:
- Use that feature directly

If no ID:
- Get current git branch
- Search `.specs/*/spec.md` for matching `branch:` in frontmatter
- If found, use that feature
- If not found:
  - If only one feature exists, use it
  - If multiple, list them and ask user to specify

### Step 2: Load Plan

Read `.specs/{ID}-{feature}/plan.md`

If file doesn't exist, inform user to run `/plan` first.

### Step 3: Generate Tasks

Invoke the `task-generator` agent with:
- The technical plan
- Feature ID and name

The agent will create `.specs/{ID}-{feature}/tasks.md` with:
- Sequential IDs (T001, T002...)
- Dependency markers [P] and [B:Txxx]
- Categories (Setup, Core, Testing, Polish)
- Checkboxes for tracking

### Step 4: Report

Inform the user:
- Tasks created at `.specs/{ID}-{feature}/tasks.md`
- Next step: `/spec-driven:implement` to start implementation

Show a summary table:
```
## Task Summary

| Category | Tasks | Complexity |
|----------|-------|------------|
| Setup & Dependencies | T001-T002 | Low |
| Core Implementation | T003-T006 | High |
| Testing & Validation | T007-T008 | Medium |
| Polish & Documentation | T009 | Low |

Run `/spec-driven:implement` to start, or `/spec-driven:implement T001` for a specific task.
```

## Error Handling

- **Feature not found**: List available features or suggest `/spec-driven:init`
- **Plan not found**: Inform user to run `/spec-driven:plan` first
- **Plan incomplete**: Point out missing sections, suggest updating plan
