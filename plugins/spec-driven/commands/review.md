---
description: Review code changes and summarize work
argument-hint: (none)
---

# Review Command

Review code changes with confidence-based filtering and present a summary of the work completed.

## Process

### Step 1: Load Context

Get current branch:
```bash
git branch --show-current
```

Read:
- `.specs/{branch}/spec.md` - Requirements (extract Acceptance Criteria section)
- `.specs/{branch}/plan.md` - Architectural decisions made
- `.specs/{branch}/tasks.md` - What was implemented

### Step 2: Review Code

Invoke the `code-reviewer` agent with:
- **Specification** (spec.md - Acceptance Criteria section)
- **Technical plan** (plan.md - Architecture Decision section)
- git diff of changes

The agent will:
- Review all changes (git diff)
- Check against project guidelines (CLAUDE.md)
- **Validate acceptance criteria from spec.md**
- **Verify architectural decisions from plan.md**
- Detect bugs, security issues, quality problems
- Only report issues with confidence >= 80

### Step 3: Present Findings

Show the review results:
- Critical issues (must fix)
- Important issues (should fix)
- Summary and recommendation

### Step 4: Generate Summary

Present a summary of the feature implementation:

```markdown
## Feature Summary: {feature_name}

### What Was Built
{description based on completed tasks}

### Key Decisions
{from plan.md Architecture Decision section}

### Acceptance Criteria Status
| Criterion | Status |
|-----------|--------|
| AC-001: ... | Satisfied/Partial/Missing |

### Files Modified
| File | Action |
|------|--------|
| ... | Created/Modified |

### Review Status
{issues found or ready for merge}

### Suggested Next Steps
- [ ] Fix any critical issues
- [ ] Create PR with: `gh pr create`
- [ ] Run tests if applicable
```

### Step 5: Offer to Save

Ask user if they want to save the summary to a file.

If yes, save to `.specs/{branch}/summary.md`

## Error Handling

- **No changes found**: Inform user there's nothing to review
- **Tasks incomplete**: Note which tasks are still pending
- **Critical issues**: Emphasize these must be fixed before merge
