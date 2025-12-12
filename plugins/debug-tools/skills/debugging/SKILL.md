# Debugging Skill

Guide for debugging with targeted log injection and runtime analysis.

## When to Use

Activates when users describe bugs:
- "X is not working"
- "Getting error Y when doing Z"
- "Something broke after [change]"

## Log Format

```
[DEBUG] [file:line] description { values }
```

- `[DEBUG]` - Prefix for grep and cleanup
- `[file:line]` - Location for navigation
- `description` - What this log checks
- `{ values }` - Relevant data (no sensitive info)

## Log Patterns

### React/Next.js

```javascript
// Lifecycle
console.log('[DEBUG] [Component.tsx:10] mount', { props });

// Effect
useEffect(() => {
  console.log('[DEBUG] [Component.tsx:15] effect run', { deps });
  return () => console.log('[DEBUG] [Component.tsx:17] cleanup');
}, [deps]);

// State
console.log('[DEBUG] [Component.tsx:25] setState', { prev: state, next: newValue });
```

### Node.js/Express

```javascript
// Request
console.log('[DEBUG] [route.ts:10] request', { method: req.method, path: req.path });

// Error
console.log('[DEBUG] [service.ts:30] error', { name: err.name, message: err.message });
```

### API Calls

```javascript
console.log('[DEBUG] [api.ts:10] fetch start', { url, method });
console.log('[DEBUG] [api.ts:15] fetch done', { status: res.status, ok: res.ok });
```

## Common Bug Patterns

| Pattern | Symptom | Check |
|---------|---------|-------|
| Null access | "Cannot read property X of undefined" | Optional chaining, defaults |
| Race condition | Works sometimes, fails randomly | Async ordering, state during render |
| Stale closure | Using old values in callbacks | useCallback deps, event bindings |
| API mismatch | Data not displaying | Response shape, null handling |
| Auth issues | Logged out unexpectedly | Token expiry, refresh logic |

## Cleanup

After debugging, remove all logs:

```bash
grep -rn '\[DEBUG\]' . --include='*.ts' --include='*.tsx' --include='*.js'
```

## MCP Integration

| MCP | Provides |
|-----|----------|
| Console Ninja | Runtime values, test status, coverage |
| Chrome DevTools | Network inspection, browser console, DOM state |
