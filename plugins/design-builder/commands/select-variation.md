---
description: Select a design variation to use
argument-hint: <variation-name>
---

# Select Variation Command

Select one of the generated design variations and copy it to ./src/.

## Arguments

- `<variation-name>` - Required (e.g., "editorial", "startup", "bold")

Arguments received: $ARGUMENTS

## Process

### Step 1: Validate variation exists

Check if `./outputs/{variation-name}/` directory exists.

If not found, list available variations in ./outputs/.

### Step 2: Copy to ./src/

Execute: `cp -r ./outputs/{variation}/* ./src/`

### Step 3: Inform result

- "Variation '{name}' copied to ./src/."
- "Other variations preserved in ./outputs/ (delete manually if not needed)."

## Error Handling

- **No variation name provided**: Please specify a variation name: /select editorial
- **Variation not found**: Variation '{name}' not found. Available variations: {list}
- **No outputs directory**: No variations found. Run /build-frontend --variations first
