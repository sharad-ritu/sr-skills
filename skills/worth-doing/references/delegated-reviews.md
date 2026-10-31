# Delegated reviews

When the user or existing workflow calls for a delegated review, apply `worth-doing` in both roles. Keep the chosen provider, model, and active harness's delegation rules.

## Give the reviewer enough context

Do not assume the child inherits the conversation or loaded skills. Pass:

- The skill's accessible absolute path, or its instructions if the child cannot read that path.
- The repository, reviewed paths, and base or diff when reviewing a change. Include relevant untracked files.
- The goal, acceptance criteria, known constraints, and what is outside scope.
- Checks already performed and their limitations, without claiming they prove more than they do.
- The review-only boundary and any read-only or chat-only limits already in force.

A brief can use this shape:

```text
Review only. Do not edit, commit, push, or start additional reviewers.
Use worth-doing at <absolute-path-to-skill>/SKILL.md.
Repository: <path>. Review scope: <paths and base, or feature>.
Goal: <intended behavior or improvement>.
Constraints and exclusions: <relevant limits>.
Checks and limitations: <observed results>.
Return only worthwhile findings and consequential unresolved questions.
For each finding, provide an ID, decision, location, evidence,
concrete benefit or failure path, and smallest sufficient recommendation.
```

Make the brief specific to the actual task.

## Assess and bound follow-up

The receiving agent checks recommendations independently using the skill's criteria. Preserve finding IDs. In a recheck brief, record acceptance, narrowing, or rejection with a short reason. Include this record in the report only when the user asks to audit decisions.

Use the enclosing workflow's review budget. If it has none, allow an initial review and at most one focused recheck. Recheck changed behavior or consequential open findings, not the whole codebase. Declined suggestions and wording-only changes do not need another round.

If disagreement remains, present the evidence and unresolved consequence briefly. A reviewer timeout, exhausted budget, or lack of response is not approval. Another round requires new evidence within the user's scope and remaining review budget.
