---
name: jira-to-tickets
description: Break a plan, spec, or the current conversation into tracer-bullet tickets with blocking edges, then publish them to Jira.
---

# Jira To Tickets

Break a plan, spec, or the current conversation into a set of **tickets**:
tracer-bullet vertical slices, each declaring the tickets that **block** it.

## Process

### 1. Gather context

Work from whatever is already in the conversation context. If the user passes
a reference (a spec path, Jira key, or URL) as an argument, fetch it and read
its full body and comments.

### 2. Explore the codebase

If you have not already explored the codebase, do so to understand the current
state of the code. Ticket titles and descriptions should use the project's
domain glossary vocabulary and respect ADRs in the area you're touching.

Look for opportunities to prefactor the code to make the implementation easier.
"Make the change easy, then make the easy change."

### 3. Draft vertical slices

Break the work into **tracer bullet** tickets.

- Each slice cuts a narrow but COMPLETE path through every layer (schema, API,
  UI, tests): vertical, NOT a horizontal slice of one layer.
- A completed slice is demoable or verifiable on its own.
- Each slice is sized to fit in a single fresh context window.
- Any prefactoring should be done first.

Give every ticket its blocking edges: only tickets that genuinely gate its
start. A ticket with no blockers can start immediately.

**Wide refactors are the exception to vertical slicing.** A **wide refactor**
is one mechanical change whose **blast radius** fans across the codebase, so no
vertical slice can land green. Sequence it as **expand--contract**: first
expand by adding the new form beside the old, then migrate callers in batches
sized by blast radius, and finally contract by deleting the old form once no
callers remain. Each migrate batch is blocked by expand, and contract is
blocked by every migrate batch. When batches cannot stay green alone, use a
shared integration branch and a final integrate-and-verify ticket.

### 4. Quiz the user

Present the proposed graph as a numbered list. For each ticket show:

- **Title:** a short descriptive name.
- **Blocked by:** the tickets that genuinely gate it.
- **What it delivers:** end-to-end behavior, not a layer-by-layer task list.

Ask the user:

- Does the granularity feel right? (too coarse / too fine)
- Are the blocking edges correct: does each ticket only depend on tickets that
  genuinely gate it?
- Should any tickets be merged or split further?

Iterate until the user approves the breakdown.

### 5. Publish to Jira

Publish the approved tickets to Jira. Create one Jira issue per ticket in
dependency order, blockers first, so each blocking edge can reference a real
issue. Use Jira's native blocking or sub-task relationship where the selected
project supports it; otherwise set each ticket's `Blocked by` field to its
blockers. Apply the `ready-for-agent` label when that label exists in the
selected Jira project. Work the **frontier**: any ticket whose blockers are all
done. Do NOT close or modify a parent issue.

Avoid brittle file paths and ordinary code snippets. If a prototype contains a
state machine, reducer, schema, or type shape that captures a decision more
precisely than prose, include only that decision-rich fragment and identify it
as a prototype result.

Use this Jira issue body:

## Parent

A reference to the parent issue on Jira, if the source was an existing issue;
otherwise omit this section.

## What to build

The end-to-end behavior this ticket makes work, from the user's perspective,
not a layer-by-layer implementation list.

## Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2

## Blocked by

- A reference to each blocking ticket, or "None (can start immediately)".
