---
description: Generate optimized prompt for design tools
argument-hint: [--target=replit|v0|lovable|figma]
---

<objective>
Generate an optimized prompt for AI design tools by invoking the prompt-generator subagent.
</objective>

<instructions>
Invoke the `prompt-generator` subagent to generate the prompt.

Arguments received: $ARGUMENTS

The prompt-generator will:
1. Locate copy.yaml and design.json
2. Use --target if provided, otherwise ask user
3. Generate prompt-{target}.md optimized for the platform

Wait for the agent to complete and inform the user of the result.
</instructions>

<error_handling>
- **No copy.yaml found**: "Run /extract-copy first to create content structure."
- **No design.json found**: "Run /extract-design first to extract design tokens."
- **Invalid target**: "Valid targets: replit, v0, lovable, figma."
</error_handling>
