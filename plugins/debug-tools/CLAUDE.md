# debug-tools

Claude Code plugin for debugging with code analysis and runtime inspection.

## Overview

Systematic debugging through:
- Code investigation to find root cause
- Targeted log injection with `[DEBUG]` prefix
- Runtime analysis via Console Ninja and Chrome DevTools MCP
- Automatic cleanup of debug logs

## Architecture

```
debug-tools/
├── .claude-plugin/
│   └── plugin.json
├── .mcp.json                  # Console Ninja + Chrome DevTools + Serena
├── agents/
│   ├── bug-investigator.md    # Investigates and finds root cause
│   └── log-injector.md        # Adds targeted debug logs
├── commands/
│   └── debug.md               # Main entry point
└── skills/
    └── debugging/
        └── SKILL.md           # Framework-specific patterns
```

## Workflow

```
/debug "bug description"
    |
    v
Bug Investigator analyzes code
    |
    v
Finds root cause (or requests runtime data)
    |
    v
If needed: Log Injector adds targeted logs
    |
    v
Proposes fix -> User approves -> Apply
    |
    v
Cleanup debug logs
```

## Command

| Command | Description |
|---------|-------------|
| `/debug "description"` | Start debugging session |

## Agents

| Agent | Role |
|-------|------|
| `bug-investigator` | Investigates code, finds root cause, proposes fix |
| `log-injector` | Adds targeted debug logs when runtime data needed |

## MCP Integration

Optional MCP servers for enhanced debugging:

| MCP | Purpose |
|-----|---------|
| Console Ninja | Runtime values, test status, code coverage |
| Chrome DevTools | Network inspection, browser console, DOM |
| Serena | Semantic code analysis via LSP |

### Setup

```bash
# Console Ninja (requires VS Code extension)
claude mcp add console-ninja -s project -- npx "-y" "-c" "node ~/.console-ninja/mcp"

# Chrome DevTools (requires Chrome remote debugging)
claude mcp add chrome-devtools -s project -- npx -y @anthropic/chrome-devtools-mcp

# Serena (requires uvx)
claude mcp add serena -s project -- uvx --from git+https://github.com/oraios/serena serena start-mcp-server --enable-web-dashboard false
```

## Log Format

```javascript
console.log('[DEBUG] [file:line] description', { values });
```

## Cleanup

Debug logs are removed when bug is fixed:

```bash
grep -rn '\[DEBUG\]' . --include='*.ts' --include='*.tsx' --include='*.js'
```

## Example

```
User: /debug "Form submission fails silently"

Agent: [Investigates form component, submit handler, API calls]

Found the issue. In `components/Form.tsx:45`, the catch block
swallows the error without updating state:

```typescript
catch (error) {
  // error silently ignored
}
```

Proposed fix:
```diff
catch (error) {
-  // error silently ignored
+  setError(error.message);
}
```

Apply this fix?

User: Yes

Agent: Fixed. Try submitting the form again.

User: Works!

Agent: Done.
```
