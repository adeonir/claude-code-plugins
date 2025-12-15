---
description: Execute implementation tasks
argument-hint: [T001 | T001-T005 | --all]
---

# Implement Command

Execute tasks from the task list, respecting dependencies and updating progress.

## Arguments

| Input | Action |
|-------|--------|
| (empty) | Next pending task |
| `T001` | Single task |
| `T001-T005` | Range of tasks |
| `--all` | All pending tasks |

Arguments received: $ARGUMENTS

## Process

### Step 1: Load Context

Get current branch:
```bash
git branch --show-current
```

Read:
- `.specs/{branch}/plan.md` - Technical decisions
- `.specs/{branch}/tasks.md` - Task list and progress

If files don't exist, inform user to run `/spec-driven:plan` and `/spec-driven:tasks` first.

### Step 2: Parse Scope

Determine which tasks to execute based on arguments.

### Step 3: Validate Dependencies

For each task to execute:
- If marked `[P]`, can proceed
- If marked `[B:Txxx]`, check if Txxx is completed
- Skip blocked tasks, inform user

### Step 4: Execute Tasks

Invoke the `implement-agent` with:
- Task scope
- Technical plan
- Current task list

The agent will:
- Implement each task following the plan
- Update tasks.md with checkboxes
- Suggest atomic commits

### Step 5: Report

After execution:
- Show tasks completed
- Show files created/modified
- Show remaining tasks
- Suggest commit message
- Next steps: continue with `/spec-driven:implement` or `/spec-driven:review` when done

## Error Handling

- **Plan/tasks not found**: Inform user to run previous commands
- **Dependency blocked**: List which tasks need to complete first
- **Implementation error**: Report issue, keep task unchecked
