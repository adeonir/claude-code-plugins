---
description: Start debugging session with investigation and targeted logging
argument-hint: "bug description"
allowed-tools: Glob, Grep, Read, Write, Edit, Bash, Task
---

# Debug Command

Start a debugging session.

## Flow

1. Use `bug-investigator` to find the root cause
2. If runtime data needed, use `log-injector` for targeted logs
3. When cause confirmed, propose fix
4. After fix verified, cleanup debug logs

## Notes

- The investigator may ask clarifying questions
- Logs are temporary - always cleanup after
