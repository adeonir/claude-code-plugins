# PR Guidelines

## Types

| Type | Use when |
|------|----------|
| `feat` | Adding new functionality |
| `fix` | Fixing a bug |
| `refactor` | Restructuring code without changing behavior |
| `chore` | Maintenance tasks, dependencies, configs |
| `docs` | Documentation changes |
| `test` | Adding or updating tests |

## Format

**Title:**
```
type: concise description in imperative mood
type(scope): concise description  # scope is optional
```

**Body:**
```markdown
Brief summary of what this PR does (2-3 sentences max).

## Changes
- Key change 1
- Key change 2
- Key change 3
```

## Guidelines

- Analyze commits and diff, not conversation context
- Title and description should reflect the current implementation state
- Be specific about functionality, not generic
- Focus on WHAT is being done, not HOW
- Use imperative mood: "add", "fix", "implement"
- Keep changes list to 3-5 key items
- Do not include risk assessment, testing instructions, or technical flow sections

## Examples

**Simple PR:**
```
Title: fix(ui): resolve pagination reset on filter change

Body:
Fixes an issue where pagination would reset to page 1 when applying filters,
causing users to lose their position in the results.

## Changes
- Preserve page state when filters change
- Reset only when search query changes
```

**Feature PR:**
```
Title: feat: add user session timeout handling

Body:
Implements automatic session timeout to improve security. Users are warned
before timeout and automatically logged out after inactivity period.

## Changes
- Session monitoring with activity tracking
- Warning dialog before session expiration
- Automatic logout after inactivity period
- User preference for timeout duration
```
