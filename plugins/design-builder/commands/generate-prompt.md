---
description: Generate optimized prompt for design tools
argument-hint: [--target=replit|v0|lovable|figma]
---

# Generate Prompt Command

Generate an optimized prompt for AI design tools.

## Arguments

- `--target` - Target platform (replit, v0, lovable, figma)

Arguments received: $ARGUMENTS

## Process

Invoke the `prompt-generator` subagent to generate the prompt.

The prompt-generator will:
1. Locate copy.yaml and design.json
2. Use --target if provided, otherwise ask user
3. Generate prompt-{target}.md optimized for the platform

Wait for the agent to complete and inform the user of the result.

## Error Handling

- **No copy.yaml found**: Ask user for brief project description
- **No design.json found**: Run /extract-design first to extract design tokens
- **Invalid target**: Valid targets: replit, v0, lovable, figma
