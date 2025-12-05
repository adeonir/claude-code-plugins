# Commit Guidelines

## Types

| Type | Use when |
|------|----------|
| `feat` | Adding new functionality |
| `fix` | Fixing a bug |
| `refactor` | Restructuring code without changing behavior |
| `chore` | Maintenance tasks, dependencies, configs |
| `docs` | Documentation changes |
| `test` | Adding or updating tests |

## Message Format

```
type: concise description in imperative mood

- Optional: area or component affected
- Optional: another key change
```

## Guidelines

- Analyze the actual diff, not the conversation context
- Message should reflect the current state of the implementation
- Be specific about functionality, not generic
- Focus on WHAT is being done, not HOW
- Use imperative mood: "add", "fix", "implement"
- Do not mention specific files or technical decisions
- Do not reference future tasks or architectural reasoning

## Body

Include a body only when the change spans 3+ functional areas. Keep it to 3-4 concise list items describing implementation areas, not files.

## Examples

Single-area change:
```
fix: resolve pagination reset on filter change
```

Multi-area change:
```
feat: add user session timeout handling

- Session monitoring with activity tracking
- Automatic logout after inactivity period
- Warning dialog before session expiration
```
