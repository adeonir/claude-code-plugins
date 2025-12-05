---
description: Create PR with generated title and description
argument-hint: [base-branch]
allowed-tools: Bash(git:*), Bash(gh:*), Bash(which gh)
---

# Create PR Command

Generate PR details and create the Pull Request directly via `gh` cli.

## Arguments

- **No argument**: Auto-detect base branch (main > master > develop)
- **`base-branch`**: Use specified branch as base for comparison

## Process

1. **Check gh cli availability**:
   ```bash
   which gh
   ```
   If not available, stop and inform user to install `gh` cli or use `/details` instead.

2. **Detect base branch** (if not specified):
   ```bash
   git branch -a | grep -E "(main|master|develop)$" | head -1
   ```

3. **Gather context** (run in parallel):
   ```bash
   git branch --show-current
   git log {base}..HEAD --oneline
   git diff {base}...HEAD --stat
   git diff {base}...HEAD
   ```

4. **Analyze changes**:
   - Review commits and diff to understand what changed
   - Base analysis solely on file contents, not conversation context
   - Determine the appropriate PR type

5. **Create PR**:
   ```bash
   gh pr create --title "type: description" --body "..."
   ```

## Format and Guidelines

See `templates/pr-guidelines.md` for:
- PR types
- Title and body format
- Guidelines
- Examples

## Task

Generate PR details for current branch with $ARGUMENTS and create PR using `gh pr create`.

Output the PR URL when done.
