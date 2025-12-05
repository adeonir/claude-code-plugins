---
description: Generate task list from technical plan
argument-hint: (none)
---

<objective>
Transform the technical plan into an organized, trackable task list.
</objective>

<instructions>
Generate a task list from the technical plan.

## Step 1: Load Plan

Get current branch:
```bash
git branch --show-current
```

Read `.specs/{branch}/plan.md`

If file doesn't exist, inform user to run `/plan` first.

## Step 2: Generate Tasks

Invoke the `task-generator` agent with:
- The technical plan
- Current branch name

The agent will create `.specs/{branch}/tasks.md` with:
- Sequential IDs (T001, T002...)
- Dependency markers [P] and [B:Txxx]
- Categories (Setup, Core, Testing, Polish)
- Checkboxes for tracking

## Step 3: Report

Inform the user:
- Tasks created at `.specs/{branch}/tasks.md`
- Next step: `/implement` to start implementation

Show a summary table:
```
## Task Summary

| Category | Tasks | Complexity |
|----------|-------|------------|
| Setup & Dependencies | T001-T002 | Low |
| Core Implementation | T003-T006 | High |
| Testing & Validation | T007-T008 | Medium |
| Polish & Documentation | T009 | Low |

Run `/implement` to start, or `/implement T001` for a specific task.
```
</instructions>

<error_handling>
- **Plan not found**: Inform user to run `/plan` first
- **Plan incomplete**: Point out missing sections, suggest updating plan
</error_handling>
