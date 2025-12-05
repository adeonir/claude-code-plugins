# git-helpers

Git workflow helper commands for Claude Code.

## Commands

| Command | Description |
|---------|-------------|
| `/commit` | Create commits with well-formatted messages |
| `/commit -s` | Commit only staged files |
| `/pr-description` | Generate PR title and description |
| `/code-review` | Review code changes for issues |

## Agents

| Agent | Description |
|-------|-------------|
| `code-reviewer` | Senior code reviewer for quality analysis |

## Installation

```bash
/plugin install git-helpers
```

## Usage

### /commit

Create a commit with an auto-generated message based on the actual diff.

```bash
/commit           # Stage all files and commit
/commit -s        # Commit only staged files
```

**Message format:** `type: concise description`

**Types:** `feat`, `fix`, `refactor`, `chore`, `docs`, `test`

### /pr-description

Generate PR title and description comparing current branch to base.

```bash
/pr-description          # Auto-detect base branch
/pr-description main     # Use main as base
```

**Output:**
- If `gh` cli available: creates PR directly
- Otherwise: saves to `PR_DETAILS.md`

### /code-review

Review code changes using the `code-reviewer` agent.

```bash
/code-review          # Auto-detect base branch
/code-review main     # Use main as base
```

**Output:** `CODE_REVIEW.md` with issues, suggestions, and summary.

## Key Principles

- Analyzes actual file changes, not conversation context
- Messages reflect current implementation state
- Concise, actionable output
- No unnecessary sections or verbose templates

## License

MIT
