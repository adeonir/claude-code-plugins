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
- `.specs/{branch}/spec.md` - Requirements (extract Acceptance Criteria section)
- `.specs/{branch}/plan.md` - Technical decisions and Critical Files
- `.specs/{branch}/research.md` - External research (if exists, extract key findings summary)
- `.specs/{branch}/tasks.md` - Task list and progress

If plan.md or tasks.md don't exist, inform user to run `/spec-driven:plan` and `/spec-driven:tasks` first.

### Step 1.5: Load Critical Files

From plan.md, identify the `## Critical Files` section.

For the tasks about to execute:
- Read the **Reference Files** relevant to current tasks (max 5 files)
- These provide patterns and conventions to follow during implementation

This ensures the implement-agent has concrete examples to follow.

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
- **Specification** (spec.md - Acceptance Criteria section)
- Technical plan (plan.md)
- **Research findings** (research.md summary, if exists)
- Current task list (tasks.md)
- **Reference file contents** (patterns to follow for current tasks)
- Current branch name

The agent will:
- Implement each task following the plan
- Validate against acceptance criteria
- Follow patterns from reference files
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
