---
description: Review code changes using code-reviewer agent
argument-hint: [base-branch]
---

# Code Review Command

Review code changes using the `code-reviewer` agent.

## Arguments

- **No argument**: Review uncommitted changes (staged + unstaged), or branch diff if on a feature branch
- **`base-branch`**: Compare current branch against specified base branch (e.g., `development`, `main`)

## Context

- Current branch: !`git branch --show-current`
- Arguments provided: `$ARGUMENTS`

## Task

1. **Determine base branch**:
   - If `$ARGUMENTS` is provided and non-empty: use it as base branch (e.g., if user passed `development`, use `development`)
   - If no argument: auto-detect by checking which exists: `development` -> `develop` -> `main` -> `master`
   - Store this as `BASE_BRANCH` for use in the review

2. **Detect review mode**:
   - Run `git status --porcelain` to check for uncommitted changes
   - If there are uncommitted changes: review those files (working directory changes)
   - If no uncommitted changes: compare current branch against `BASE_BRANCH`

3. **Get modified files and diff**:
   - For uncommitted changes:
     - Files: `git diff --name-only` (unstaged) and `git diff --cached --name-only` (staged)
     - Diff: `git diff` and `git diff --cached`
   - For branch comparison:
     - Files: `git diff $BASE_BRANCH...HEAD --name-only`
     - Diff: `git diff $BASE_BRANCH...HEAD`

4. **Launch code-reviewer agent**: Pass the following context:
   - The base branch being compared against (IMPORTANT: must match what user requested)
   - The list of modified files
   - The actual diff content for context

5. **Important**: The review header MUST show the correct base branch. If user passed `development` as argument, the review should say "Reviewed against `development`", not `master` or any other branch.
