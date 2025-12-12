---
description: Create feature specification from description or PRD
argument-hint: <description> | @<file.md>
---

# Spec Command

Transform a feature description or PRD into a structured specification file.

## Arguments

- `<description>` - Text describing the feature
- `@<file.md>` - Path to PRD file to use as context

Arguments received: $ARGUMENTS

## Process

### Step 1: Confirm Branch

Get the current git branch:
```bash
git branch --show-current
```

Show the branch to the user and ask if they want to:
- Continue on this branch
- Create/switch to a new branch

### Step 2: Process Input

If input is a file reference (@file.md):
- Read the file content as PRD context

If input is text:
- Use as feature description

If input is empty:
- Ask the user for a feature description

### Step 3: Generate Specification

Create `.specs/{branch}/spec.md` using the template from `templates/spec.md`:

Extract from the input:
- **Feature name**: Clear, concise name
- **Overview**: Brief description of what this feature does
- **User Stories**: Format as "As a {user}, I want {goal} so that {benefit}"
- **Functional Requirements**: Specific capabilities (FR-001, FR-002...)
- **Acceptance Criteria**: Testable conditions (AC-001, AC-002...)

### Step 4: Mark Ambiguities

For any unclear or underspecified items, add:
```
[NEEDS CLARIFICATION: specific question]
```

### Step 5: Report

Inform the user:
- Spec file created at `.specs/{branch}/spec.md`
- Number of items needing clarification (if any)
- Next step: `/clarify` to resolve ambiguities, or `/plan` if none

## Error Handling

- **No input provided**: Ask user for feature description
- **File not found**: Inform user and ask for correct path
- **Branch issue**: Suggest creating a new branch for the feature
