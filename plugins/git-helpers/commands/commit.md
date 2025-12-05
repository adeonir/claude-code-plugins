---
description: Create commits with well-formatted messages
argument-hint: [-s|--staged]
allowed-tools: Bash(git:*)
---

# Commit Command

Create a commit with a well-formatted message based on the actual file changes.

## Arguments

- **No flag**: Stage all modified/new files before committing
- **`-s` or `--staged`**: Use only files already staged

## Process

1. **Gather context** (run in parallel):
   ```bash
   git status
   git diff HEAD
   git log --oneline -5
   ```

2. **Analyze changes**:
   - Review the diff output to understand what changed
   - Base your analysis solely on the file contents, not conversation context
   - Determine the appropriate commit type

3. **Stage files** (if not using `-s/--staged`):
   ```bash
   git add .
   ```

4. **Create commit** using HEREDOC format:
   ```bash
   git commit -m "$(cat <<'EOF'
   type: concise description

   - Optional body item 1
   - Optional body item 2
   EOF
   )"
   ```

5. **Verify commit**:
   ```bash
   git log -1 --format="%B"
   git status
   ```

6. **Handle pre-commit hooks** (if files were modified):
   - Check authorship: `git log -1 --format='%an %ae'`
   - If safe, amend the commit with modified files (one retry only)

## Format and Guidelines

See `templates/commit-guidelines.md` for:
- Commit types
- Message format
- Guidelines
- Examples

## Task

Create a commit for changes with $ARGUMENTS.

Use only git commands. Do not use other tools or send additional messages beyond the tool calls.
