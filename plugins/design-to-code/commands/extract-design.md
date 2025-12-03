---
description: Extract design tokens from reference images to design.json
argument-hint: [image-url...]
---

<objective>
Extract design tokens from reference images and generate a design.json file by invoking the design-extractor subagent.
</objective>

<instructions>
Invoke the `design-extractor` subagent to extract design tokens from images.

Arguments received: $ARGUMENTS

The design-extractor will:
1. Request images from user if not provided
2. Locate existing copy.yaml for project context
3. Extract colors, typography, spacing, components
4. Generate design.json in the same folder as copy.yaml

Wait for the agent to complete and inform the user of the result.
</instructions>

<error_handling>
- **No images provided**: Ask user to paste reference images.
- **No copy.yaml found**: "Run /extract-copy first to create content structure."
</error_handling>
