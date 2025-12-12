---
description: Resolve ambiguities in the specification
argument-hint: (none)
---

# Clarify Command

Identify and resolve items marked [NEEDS CLARIFICATION] in the specification.

## Process

### Step 1: Load Specification

Get current branch and read the spec:
```bash
git branch --show-current
```

Read `.specs/{branch}/spec.md`

If file doesn't exist, inform user to run `/spec` first.

### Step 2: Find Clarifications Needed

Search for all `[NEEDS CLARIFICATION: ...]` markers in the spec.

If none found:
- Inform user the spec is complete
- Suggest running `/plan` next
- Exit

### Step 3: Present Questions

For each clarification needed:
- Present the question clearly
- Provide context from the surrounding spec content
- Suggest options if applicable

Use AskUserQuestion for structured choices when appropriate.

### Step 4: Update Specification

For each answered question:
- Replace the `[NEEDS CLARIFICATION: ...]` marker with the clarified content
- Keep the spec well-formatted

### Step 5: Report

After all clarifications:
- Show summary of what was clarified
- Check if any new clarifications emerged
- Suggest `/plan` as next step if spec is complete

## Error Handling

- **Spec not found**: Inform user to run `/spec` first
- **User unsure**: Mark as still needing clarification, move on
- **Conflicting answers**: Ask for resolution before proceeding
