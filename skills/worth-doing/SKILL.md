---
name: worth-doing
description: "Judge which recommendations are worth acting on. Use when the user says 'worth doing' or 'worth-doing', or when assessing review feedback."
---

# Worth doing

Recommend changes whose concrete benefit justifies their cost in this project. Apply this discipline both when producing a review and when deciding whether to accept one.

## Establish the scope

Identify the user's goal, the code or feature under review, and relevant constraints. Judge against that scope. Distinguish issues introduced by a change from existing issues rather than treating every nearby problem as a regression.

This skill evaluates recommendations. It does not authorize implementation, delegation, commits, or external actions. Preserve existing authorization and limits.

## Assess each recommendation

Read the relevant implementation and callers before accepting a claim. Ask:

- What current behavior, requirement, or maintenance problem would this address?
- For a bug, what credible input or execution path triggers it? What existing validation or invariant prevents it, and is there a relevant bypass?
- For an improvement, what becomes simpler, faster, easier to change, or more useful now? An improvement need not prevent a failure, but speculative future flexibility is insufficient.
- How much does the benefit matter at relevant usage? Weigh it against implementation effort, added complexity, and regression risk.
- What is the smallest sufficient change? Consider deletion, narrowing the change, or using an existing mechanism before adding an abstraction or defensive check.

A nullable schema or permissive type alone does not establish a reachable bug. Check relevant write paths, validation, and existing data when they affect the claim. Conversely, a convention or a few valid rows do not prove invalid data impossible.

Keep likelihood, impact, and confidence distinct, and state each in words backed by evidence. A rare but credible authorization failure or data-loss scenario may matter greatly. A cheap fix is not worthwhile merely because it is cheap. Performance claims need evidence relevant to actual usage; simplification can be justified by the code itself.

## Decide what deserves attention

Assign each candidate one decision:

- **Do now.** Evidence supports a meaningful benefit within the current scope, at a justified cost.
- **Follow up.** A worthwhile issue belongs outside this task. Surface it only if its importance justifies interrupting the user. Create a ticket only when requested.
- **Investigate.** A specific missing fact could change the decision. Make a targeted check within the authorized scope. If it remains unresolved, report the uncertainty only when consequential, without presenting it as a proven defect or a clean result.
- **Omit.** The claim is unsupported, already prevented, irrelevant, or costs more than it helps.

Filter before reporting. The report carries only Do now findings and the Follow up and Investigate items that earned the user's attention.

## Produce or assess a review

As the reviewer, substantiate and filter your own recommendations before returning them.

As the receiving agent, independently check each recommendation against the code and scope. Accept, narrow, or decline it with evidence. The reviewer's confidence or severity label is not authority. Change code for evidence, never just to obtain approval. Distinguish changes required for correctness or acceptance from optional improvements. A worthwhile improvement is not automatically a release blocker.

When delegating or assessing a delegated review, read [Delegated reviews](references/delegated-reviews.md) for what to pass to the reviewer and how to bound follow-up rounds. This skill supplements the chosen review workflow and model, rather than replacing them.

## Report and stop

Read and apply the `unslop` skill to the report. If it is not in the available skills list, read `../unslop/SKILL.md` relative to this skill's directory. If neither exists, write in plain, direct language.

Lead with worthwhile findings, highest impact first. For each, give a stable ID, decision, location, concrete problem or benefit, supporting evidence, and smallest sufficient recommendation. Keep it concise. Skip empty sections and rejected-finding inventories unless the user asks to audit the decisions.

Stop when the scoped review and any consequential uncertainties are reported. If nothing qualifies, that is a valid outcome: say that no worthwhile changes were identified within the reviewed scope. State material review limitations.
