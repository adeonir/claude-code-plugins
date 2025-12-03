---
description: Build React + Tailwind components from copy.yaml and design.json
argument-hint: [--output=path]
---

<objective>
Build production-grade React components using Claude Code by invoking the frontend-builder subagent.
</objective>

<instructions>
Invoke the `frontend-builder` subagent to build the frontend.

Arguments received: $ARGUMENTS

The frontend-builder will:
1. Check if Vite project exists
2. Scaffold new project if needed (Vite + React + Tailwind + shadcn/ui)
3. Locate copy.yaml and design.json
4. Generate components applying the frontend-design skill

Wait for the agent to complete and inform the user of the result.
</instructions>

<error_handling>
- **No copy.yaml found**: "Run /extract-copy first to create content structure."
- **No design.json found**: "Run /extract-design first to extract design tokens."
- **Scaffold failed**: Check pnpm is installed and available.
</error_handling>
