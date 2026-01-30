---
name: work-and-review-loop
description: Work on tasks with iterative senior review until approved
---

# Work and Review Loop

Execute tasks with an iterative review cycle: clarify, work, get reviewed by a domain senior, fix feedback, repeat until approved.

## Process

```dot
digraph work_review_loop {
    rankdir=TB;

    "0. Clarify any ambiguity with the instructor" [shape=box];
    "Everything clear?" [shape=diamond];
    "1. Work on the task" [shape=box];
    "2. Get reviewed by a senior in that field" [shape=box];
    "Feedback exists?" [shape=diamond];
    "Done" [shape=ellipse];

    "0. Clarify any ambiguity with the instructor" -> "Everything clear?";
    "Everything clear?" -> "0. Clarify any ambiguity with the instructor" [label="no"];
    "Everything clear?" -> "1. Work on the task" [label="yes"];
    "1. Work on the task" -> "2. Get reviewed by a senior in that field";
    "2. Get reviewed by a senior in that field" -> "Feedback exists?";
    "Feedback exists?" -> "0. Clarify any ambiguity with the instructor" [label="yes - clarify feedback first"];
    "Feedback exists?" -> "Done" [label="no"];
}
```

## Steps

0. **Clarify**: If anything is unclear, ask the instructor questions until everything is crystal clear
1. **Work**: Complete the assigned task(s)
2. **Review**: Dispatch a senior-level reviewer subagent in that domain to review your work
3. **Iterate or Finish**:
   - If feedback exists: Return to step 0 to clarify the feedback, then fix
   - If no feedback: Task complete

## Important Rules

- **Never proceed with ambiguity**: If requirements, scope, approach, or feedback are unclear, stop and ask the instructor
- **Keep asking until clear**: Don't assume or guess. Ask follow-up questions until you fully understand
- **Review is mandatory**: Always get senior review before marking complete
- **Clarify feedback too**: When you receive review feedback, make sure you understand it before fixing

## Reviewer Subagent

When dispatching the reviewer, use the Task tool with a prompt like:

```
You are a senior {domain} engineer. Review the following work:

{work description and context}

Files changed: {list of files}

Provide feedback on:
- Correctness
- Best practices
- Code quality
- Edge cases

If everything looks good, respond with "APPROVED". Otherwise, list specific issues to fix.
```

## Example

```
You: I need to implement the authentication feature

[Step 0: Clarify]
You: "Should this support OAuth, or just email/password?"
Instructor: "Email/password only for now"

You: "Should we include 'forgot password' flow?"
Instructor: "Yes, with email verification"

[Step 1: Work - now clear, proceed]
[Implement login flow with forgot password]

[Step 2: Review]
[Dispatch senior backend reviewer]
Reviewer: Issues found:
- Missing rate limiting
- Password reset token expiration unclear

[Step 0: Clarify feedback]
You: "For rate limiting, how many attempts before lockout?"
Instructor: "5 attempts, then 15 minute lockout"

You: "Password reset token - 15 minutes expiration?"
Instructor: "Yes, 15 minutes"

[Step 1: Work - fix with clarity]
[Apply fixes with clear requirements]

[Step 2: Review again]
[Dispatch senior backend reviewer again]
Reviewer: APPROVED

Done!
```
