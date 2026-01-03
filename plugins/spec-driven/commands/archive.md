---
description: Generate docs and mark feature as archived
argument-hint: [ID]
---

# Archive Command

Generate documentation from the completed feature and mark it as archived.

## Arguments

- `[ID]` - Feature ID (optional if branch is associated)

Arguments received: $ARGUMENTS

## Process

### Step 1: Resolve Feature

If ID provided:
- Use that feature directly

If no ID:
- Get current git branch
- Search `.specs/*/spec.md` for matching `branch:` in frontmatter
- If found, use that feature
- If not found, list available features and ask user to specify

### Step 2: Validate Status

Read `.specs/{ID}-{feature}/spec.md` frontmatter.

Check status:
- If `done`: proceed
- If `review`: suggest running `/spec-driven:validate` first
- If other: inform user feature is not ready for archive

### Step 3: Load Artifacts

Read from `.specs/{ID}-{feature}/`:
- `spec.md` - Overview and feature description
- `plan.md` - Architecture decisions
- `tasks.md` - Count completed tasks

### Step 4: Check for Existing Docs

Determine target path from feature name (e.g., `add-2fa` -> `docs/features/auth.md` or new file).

If `docs/features/{relevant}.md` exists:
- Will append changelog entry to existing file

If not:
- Will create new file

### Step 5: Generate Documentation

Create/update `docs/features/{feature}.md`:

```markdown
# {Feature Title}

## Overview
{from spec.md Overview section}

## Architecture Decisions
{from plan.md Architecture Decision section}

## Changelog

### {YYYY-MM-DD}
- {Summary of changes from this feature}
- {Key additions, modifications, removals}
```

If file exists, only add new changelog entry at top of Changelog section.

### Step 6: Update Status

Update `.specs/{ID}-{feature}/spec.md` frontmatter:
- Set `status: archived`

### Step 7: Report

Inform user:
- Documentation generated/updated at `docs/features/{file}.md`
- Feature marked as archived
- User can delete `.specs/{ID}-{feature}/` manually if desired

## Error Handling

- **Feature not found**: List available features
- **Not in done status**: Suggest running `/spec-driven:validate` first
- **Missing artifacts**: Note which files are missing
