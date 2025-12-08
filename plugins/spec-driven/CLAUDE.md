# Spec-Driven

Claude Code plugin for specification-driven development with persistent artifacts.

## Architecture

```
spec-driven/
├── .claude-plugin/
│   └── plugin.json
├── .mcp.json
├── agents/
│   ├── code-explorer.md
│   ├── code-architect.md
│   ├── task-generator.md
│   ├── implement-agent.md
│   └── code-reviewer.md
├── commands/
│   ├── spec.md
│   ├── clarify.md
│   ├── plan.md
│   ├── tasks.md
│   ├── implement.md
│   └── review.md
├── templates/
│   ├── spec.md
│   ├── plan.md
│   └── tasks.md
└── .specs/{branch}/
    ├── spec.md
    ├── plan.md
    └── tasks.md
```

## Workflow

```
/spec "feature description"
    |
    +---> .specs/{branch}/spec.md
    v
/clarify (if needed)
    |
    +---> .specs/{branch}/spec.md (updated)
    v
/plan
    |
    +---> .specs/{branch}/plan.md
    v
/tasks
    |
    +---> .specs/{branch}/tasks.md
    v
/implement [T001|T001-T005|--all]
    |
    +---> code changes + tasks.md updated
    v
/review
    |
    +---> summary in conversation
```

## Commands

| Command | Description |
|---------|-------------|
| `/spec` | Create specification from description or PRD |
| `/clarify` | Resolve ambiguities marked [NEEDS CLARIFICATION] |
| `/plan` | Explore codebase and generate technical plan |
| `/tasks` | Generate task list from plan |
| `/implement` | Execute next task, or specify scope (T001, T001-T005, --all) |
| `/review` | Review code and summarize work |

## Agents

| Agent | Role |
|-------|------|
| `code-explorer` | Traces feature implementations, maps architecture |
| `code-architect` | Creates technical plans with decisive choices |
| `task-generator` | Decomposes plans into trackable tasks |
| `implement-agent` | Executes tasks respecting dependencies |
| `code-reviewer` | Reviews code with confidence-based filtering |

## Task Markers

| Marker | Meaning |
|--------|---------|
| `[P]` | Parallel-safe: can run alongside other [P] tasks |
| `[B:T001]` | Blocked: depends on T001 |
| `[B:T001,T002]` | Blocked: depends on T001 and T002 |
| `- [ ]` | Pending |
| `- [x]` | Completed |

## Persistent Artifacts

All artifacts are stored in `.specs/{branch}/`:

| File | Created By | Purpose |
|------|------------|---------|
| `spec.md` | /spec | Feature requirements and acceptance criteria |
| `plan.md` | /plan | Technical architecture and implementation map |
| `tasks.md` | /tasks | Trackable task list with dependencies |

## Serena MCP Integration

This plugin uses Serena MCP for semantic code operations.

| Phase | Tool | Benefit |
|-------|------|---------|
| /plan | find_symbol | Precise symbol location |
| /plan | find_referencing_symbols | Impact analysis |
| /implement | insert_after_symbol | Semantic edits |

### Requirements

Serena MCP is configured in `.mcp.json`. Requires `uvx` (uv tool runner) installed on the system.

## References

Based on:
- [ccspec](https://github.com/adeonir/ccspec) - Specification-driven development CLI
- [feature-dev](https://github.com/anthropics/claude-code/tree/main/plugins/feature-dev) - Claude Code's feature development plugin
- [Serena](https://github.com/oraios/serena) - Semantic code operations via LSP
