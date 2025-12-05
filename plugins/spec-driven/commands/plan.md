---
description: Explore codebase and generate technical plan
argument-hint: (none)
---

<objective>
Analyze the codebase and create a comprehensive technical plan for implementing the feature.
</objective>

<instructions>
Generate a technical plan by exploring the codebase and designing the implementation.

## Step 1: Load Specification

Get current branch:
```bash
git branch --show-current
```

Read `.specs/{branch}/spec.md`

If file doesn't exist, inform user to run `/spec` first.

## Step 2: Check for Clarifications

Search for `[NEEDS CLARIFICATION]` in the spec.

If found:
- List the items needing clarification
- Suggest running `/clarify` first
- Exit

## Step 3: Explore Codebase

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

## Step 4: Review Exploration

Read the files identified as essential by the explorers.

Synthesize insights:
- Patterns to follow
- Conventions to match
- Integration points
- Potential challenges

## Step 5: Generate Plan

Invoke the `code-architect` agent with:
- The specification
- Exploration insights
- Current branch name

The architect will create `.specs/{branch}/plan.md`

## Step 6: Report

Inform the user:
- Plan created at `.specs/{branch}/plan.md`
- Key architectural decisions made
- Next step: `/tasks` to generate task list
</instructions>

<error_handling>
- **Spec not found**: Inform user to run `/spec` first
- **Clarifications pending**: Suggest `/clarify` first
- **Codebase unclear**: Ask user for guidance on patterns to follow
</error_handling>
