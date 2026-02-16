---
name: micro-task
description: Execute implementation tasks with an iterative review loop. Use when the user requests strict work-review-apply cycles, asks for senior/tech-lead style review before commit, or runs `/micro-task`.
---

# Micro Task

Use a strict execution loop for small-to-medium implementation tasks.

## Required Loop

1. Clarify unknowns first. Keep asking until requirements are unambiguous.
2. Implement the requested change.
3. Run a tech-lead style review (bug/risk/regression focused).
4. If review feedback exists, return to step 1 and apply fixes.
5. If no feedback remains, commit.

## Operating Rules

- Prioritize correctness and behavior safety over speed.
- Keep changes minimal and scoped to the task.
- Do not skip the review step before commit.
- When available, apply `work-and-review-loop` process as the default execution pattern.

