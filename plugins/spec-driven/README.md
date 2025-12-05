# Spec-Driven

Specification-driven development workflow for Claude Code with persistent artifacts.

## Features

- Structured specification creation from descriptions or PRDs
- Codebase exploration and pattern analysis
- Technical planning with decisive architectural choices
- Task decomposition with dependency tracking
- Granular implementation (single task, range, or all)
- Confidence-based code review

## Installation

```bash
claude /plugin install spec-driven
```

## Quick Start

```bash
# 1. Create specification
claude /spec "Add user authentication with OAuth"

# 2. Resolve any ambiguities
claude /clarify

# 3. Generate technical plan
claude /plan

# 4. Create task list
claude /tasks

# 5. Implement tasks
claude /implement             # Next pending task
claude /implement T001        # Single task
claude /implement T001-T005   # Range
claude /implement --all       # All pending

# 6. Review and summarize
claude /review
```

## Commands

| Command | Description |
|---------|-------------|
| `/spec <description>` | Create feature specification |
| `/clarify` | Resolve [NEEDS CLARIFICATION] items |
| `/plan` | Explore codebase and create technical plan |
| `/tasks` | Generate task list from plan |
| `/implement [scope]` | Execute implementation tasks |
| `/review` | Review code and summarize work |

## Artifacts

All artifacts are stored in `.specs/{branch}/`:

```
.specs/
└── feature-auth/
    ├── spec.md    # Requirements and acceptance criteria
    ├── plan.md    # Technical architecture
    └── tasks.md   # Trackable task list
```

## Task Markers

Tasks use markers to indicate parallelization:

```markdown
- [ ] T001 [P] Setup auth provider        # Parallel-safe
- [ ] T002 [P] Create user schema         # Parallel-safe
- [ ] T003 [B:T001,T002] Implement login  # Blocked by T001 and T002
- [ ] T004 [B:T003] Add error handling    # Blocked by T003
```

## Workflow

```
/spec --> /clarify --> /plan --> /tasks --> /implement --> /review
  |          |           |          |            |            |
  v          v           v          v            v            v
spec.md   spec.md      plan.md   tasks.md   code +         summary
          (updated)                         tasks.md
```

## License

MIT
