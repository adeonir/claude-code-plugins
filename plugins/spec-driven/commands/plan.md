---
description: Explore codebase and generate technical plan
argument-hint: [additional instructions]
---

# Plan Command

Analyze the codebase and create a comprehensive technical plan for implementing the feature.

## Process

### Step 1: Load Specification

Get current branch:
```bash
git branch --show-current
```

Read `.specs/{branch}/spec.md`

If file doesn't exist, inform user to run `/spec-driven:spec` first.

### Step 2: Check for Clarifications

Search for `[NEEDS CLARIFICATION]` in the spec.

If found:
- List the items needing clarification
- Suggest running `/spec-driven:clarify` first
- Exit

### Step 3: Research External Information

Determine if web research is needed by checking:
1. **User provided additional instructions** with the `/plan` command
2. **Spec mentions external technologies**: libraries, frameworks, APIs, services
3. **Spec references standards or protocols** that need verification
4. **Domain-specific requirements** that need investigation

If ANY of the above apply, invoke the `web-researcher` agent with:
- The specification content
- User's additional instructions (if provided)
- List of topics extracted from the spec

The researcher will create `.specs/{branch}/research.md` with findings.

Skip this step only if:
- The spec is purely about internal code changes
- No external dependencies or integrations are mentioned
- No additional instructions were provided

### Step 4: Explore Codebase

Invoke the `code-explorer` agent to analyze the codebase:

Ask it to explore:
- Similar existing features
- Architecture patterns and conventions
- Relevant entry points and integration areas
- Testing patterns

You may launch 2-3 explorer agents in parallel with different focuses:
- One for similar features
- One for architecture overview
- One for integration points

### Step 5: Review Exploration

Read the files identified as essential by the explorers.

**Consolidate Critical Files:**
Collect all files marked as "essential" by each explorer and categorize them:
- **Reference Files**: Patterns to follow (existing similar features, architectural templates)
- **Files to Modify**: Existing files that need changes
- **Files to Create**: New files to be added

This consolidated list will be passed to the architect agent.

Synthesize insights:
- Patterns to follow
- Conventions to match
- Integration points
- Potential challenges

### Step 6: Generate Plan

Invoke the `code-architect` agent with:
- The specification (spec.md)
- Research findings (if research.md exists)
- Exploration insights
- **Consolidated critical files list** (Reference, Modify, Create)
- Current branch name

The architect will create `.specs/{branch}/plan.md`

### Step 7: Report

Inform the user:
- Research conducted (if applicable) at `.specs/{branch}/research.md`
- Plan created at `.specs/{branch}/plan.md`
- Key architectural decisions made
- Next step: `/spec-driven:tasks` to generate task list

## Error Handling

- **Spec not found**: Inform user to run `/spec-driven:spec` first
- **Clarifications pending**: Suggest `/spec-driven:clarify` first
- **Codebase unclear**: Ask user for guidance on patterns to follow
- **Research inconclusive**: Note uncertainties in research.md and proceed with best available information
