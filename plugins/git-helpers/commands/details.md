---
description: Generate PR title and description to file
argument-hint: [base-branch]
allowed-tools: Bash(git:*), Write
---

# PR Details Command

Generate a title and description for a Pull Request and save to `PR_DETAILS.md`.

## Arguments

- **No argument**: Auto-detect base branch (main > master > develop)
- **`base-branch`**: Use specified branch as base for comparison

## Process

1. **Detect base branch** (if not specified):
   ```bash
   git branch -a | grep -E "(main|master|develop)$" | head -1
   ```

2. **Gather context** (run in parallel):
   ```bash
   git branch --show-current
   git log {base}..HEAD --oneline
   git diff {base}...HEAD --stat
   git diff {base}...HEAD
   ```

3. **Analyze changes**:
   - Review commits and diff to understand what changed
   - Base analysis solely on file contents, not conversation context
   - Determine the appropriate PR type

4. **Save to file**:
   - Always save to `PR_DETAILS.md` in repository root

## Format and Guidelines

See `templates/pr-guidelines.md` for:
- PR types
- Title and body format
- Guidelines
- Examples

## Task

Generate PR description for current branch with $ARGUMENTS and save to `PR_DETAILS.md`.
