---
description: Create feature specification from description or PRD
argument-hint: <description> | @<file.md>
---

# Init Command

Initialize a new feature with a structured specification file.

## Arguments

- `<description>` - Text describing the feature
- `@<file.md>` - Path to PRD file to use as context
- `--link <ID>` - Associate current branch with existing feature

Arguments received: $ARGUMENTS

## Process

### Step 1: Handle --link Flag

If `--link <ID>` provided:
- Find feature with that ID in `.specs/`
- Get current git branch
- Update the feature's `spec.md` frontmatter with `branch: {current_branch}`
- Inform user and exit

### Step 2: Generate Feature ID

Scan `.specs/` directory for existing features.
Find the highest ID number and increment by 1.

Example: If `.specs/003-payment-flow/` exists, next ID is `004`.

If `.specs/` doesn't exist, start with `001`.

### Step 3: Process Input

If input is a file reference (@file.md):
- Read the file content as PRD context

If input is text:
- Use as feature description

If input is empty:
- Ask the user for a feature description

### Step 4: Process Referenced Documentation

When documentation is referenced with @path:

1. **List all files** in the referenced path
2. **Read each file completely**
3. **Extract** from each file:
   - Rules (words: "must", "cannot", "always", "never", "required")
   - Constraints (words: "only if", "when", "unless")
   - Examples (code blocks, diagrams, sample data)
4. **For each item found**, ask: "Is this relevant to the feature?"
5. **If relevant**, it MUST become an FR or AC in the spec
6. **If skipped**, note WHY in the Notes section

Output before generating spec:

```markdown
## Extracted from Documentation

| Source | Item | Relevant | Mapped To |
|--------|------|----------|-----------|
| {file} | {rule/constraint} | Yes/No | FR-xxx / AC-xxx / Skipped: {reason} |
```

### Step 5: Generate Feature Name

From the description, derive a short kebab-case name:
- "Add two-factor authentication" -> `add-2fa`
- "User registration flow" -> `user-registration`

### Step 6: Check Branch Association

Get current git branch:
```bash
git branch --show-current
```

Ask user:
- "Associate this feature with branch `{branch}`?" (Yes/No)

If on main/master, suggest creating a new branch.

### Step 7: Generate Specification

Create `.specs/{ID}-{feature}/spec.md` with frontmatter and content:

```markdown
---
id: {ID}
feature: {feature-name}
status: draft
branch: {branch or empty}
created: {YYYY-MM-DD}
---

# Feature: {Feature Title}

## Overview

{brief_description}

## User Stories

- As a {user_type}, I want {goal} so that {benefit}

## Functional Requirements

- [ ] FR-001: {requirement}
- [ ] FR-002: {requirement}

## Acceptance Criteria

- [ ] AC-001: {criterion}
- [ ] AC-002: {criterion}

## Notes

{additional_context}

<!-- Items marked [NEEDS CLARIFICATION] require resolution before plan -->
```

### Step 8: Mark Ambiguities

For any unclear or underspecified items, add:
```
[NEEDS CLARIFICATION: specific question]
```

### Step 9: Report

Inform the user:
- Feature created: `{ID}-{feature}`
- Spec file at `.specs/{ID}-{feature}/spec.md`
- Branch associated: `{branch}` (or "none")
- Number of items needing clarification (if any)
- Next step: `/spec-driven:clarify` to resolve ambiguities, or `/spec-driven:plan` if none

## Error Handling

- **No input provided**: Ask user for feature description
- **File not found**: Inform user and ask for correct path
- **ID conflict**: Should not happen, but regenerate if it does
