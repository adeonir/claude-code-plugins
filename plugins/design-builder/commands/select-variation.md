---
description: Select a design variation to use
argument-hint: <variation-name>
---

<objective>
Select one of the generated design variations and copy it to ./src/.
</objective>

<instructions>
Arguments received: $ARGUMENTS

Parse arguments:
- `variation-name`: required (e.g., "editorial", "startup", "bold")

## Process

1. **Validate variation exists**
   - Check if `./outputs/{variation-name}/` directory exists
   - If not found, list available variations in ./outputs/

2. **Copy to ./src/**
   - Execute: `cp -r ./outputs/{variation}/* ./src/`

3. **Inform result**
   - "Variation '{name}' copied to ./src/."
   - "Other variations preserved in ./outputs/ (delete manually if not needed)."

</instructions>

<error_handling>
- **No variation name provided**: "Please specify a variation name: /select editorial"
- **Variation not found**: "Variation '{name}' not found. Available variations: {list}"
- **No outputs directory**: "No variations found. Run /build-frontend --variations first."
</error_handling>
