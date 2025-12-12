---
description: Build frontend components from design tokens
argument-hint: [--variations N]
---

# Build Frontend Command

Build production-grade frontend components using Claude Code.

## Arguments

- `--variations N` - Generate N layout variations (2-3) for comparison

Arguments received: $ARGUMENTS

## Process

### If --variations is present

Invoke the `variations-builder` subagent to generate multiple design variations.

The variations-builder will:
1. Load the frontend-design skill first
2. Locate design.json (required) and copy.yaml (optional)
3. Determine variation count (default 3, max 3)
4. Detect existing project stack
5. Generate each preset (editorial, startup, bold) in ./outputs/
6. Create preview.html dynamically for side-by-side comparison
7. Inform user to open outputs/preview.html

After comparison, user can run `/select <variation-name>` to copy chosen variation to ./src/.

### If --variations is NOT present

Invoke the `frontend-builder` subagent to build a single frontend.

The frontend-builder will:
1. Detect existing project stack (React, Vue, Svelte, etc.)
2. If no project, ask user for preferred stack
3. Scaffold new project if needed
4. Locate design.json (required) and copy.yaml (optional)
5. If no copy.yaml, ask user for brief project description
6. Generate components in ./src/ applying the frontend-design skill

Wait for the agent to complete and inform the user of the result.

## Error Handling

- **No design.json found**: Run /extract-design first to extract design tokens
- **Scaffold failed**: Check package manager is installed and available
- **Variations > 3**: Maximum 3 variations supported. Generating 3 variations
