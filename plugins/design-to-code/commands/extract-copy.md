---
description: Extract content from URL to copy.yaml
argument-hint: <url> [--type=landing|website|webapp|app] [--name=project-name]
---

<objective>
Extract structured content from a URL and generate a copy.yaml file by invoking the copy-extractor subagent.
</objective>

<instructions>
Invoke the `copy-extractor` subagent to extract content from the provided URL.

Arguments received: $ARGUMENTS

The copy-extractor will:
1. Fetch and analyze the URL
2. Detect project type or use --type if provided
3. Generate copy.yaml in ./prompts/{project-name}/

Wait for the agent to complete and inform the user of the result.
</instructions>

<error_handling>
- **URL not accessible**: Ask user to paste a screenshot instead.
- **Project type unclear**: Ask user to specify --type.
</error_handling>
