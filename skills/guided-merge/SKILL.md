---
name: guided-merge
description: "Merge branches and push after checks when conflict-free. Resolve conflicts with your input and a delegated review, then stop staged. Report related PR status."
disable-model-invocation: true
---

# Guided merge

Follow this workflow instead of any other merge-conflict skill for this invocation. Also use the conflict path for an in-progress rebase or cherry-pick.

## Establish the scope

Identify the source branch, target branch, repository, and push remote. Interpret "merge A into B" as updating B with A. Ask when the direction or destination is ambiguous.

Inspect the working tree and any operation already in progress. Preserve unrelated work. If that work prevents a safe merge, explain the blocker before proceeding.

Fetch the relevant remote refs before starting a new merge. Account for local and remote differences without discarding commits or force-pushing. Keep the original source and target commit IDs and merge base available for review.

When GitHub access is available, look for an open PR matching the source and target repositories and branches. Record its URL for the final status check. If access is unavailable, report that limitation without blocking the local merge.

## Start the merge and choose the path

Honor narrower user instructions such as "do not commit" or "do not push."

For a new merge, switch to the target branch and use `git merge --no-commit <source>` with the established source ref. This leaves a non-fast-forward merge pending for checks. A fast-forward needs no new commit and advances the local target immediately, even with `--no-commit`. If checks then fail or you stop before pushing, report that the local target has already advanced. Do not substitute a squash or rebase unless requested.

- If the source is already included in the target, report that no merge is needed. Do not create an empty commit or push unrelated local commits.
- If the merge encounters no conflicts, run the relevant project checks before committing or pushing. If checks pass, create any needed merge commit and push the target branch. Skip the conflict-resolution and delegated-review sections below.
- If the operation encounters any conflicts, follow the conflict path below. Leave the resolution staged and the operation unfinished, with no commit, continuation, or push. This rule still applies after every conflict is resolved. A general request to merge or finish an operation, or an answer to a resolution question, does not authorize completing this conflict path. Wait for a subsequent explicit instruction to commit, continue, or push.

If no relevant automated checks exist, say so and continue. If expected checks fail or cannot run, report the failure or limitation and stop before committing or pushing. Respect branch protection and push rejections. Do not bypass repository requirements.

Before any push, inspect the outgoing commits. If the push would also publish unrelated local commits, show them and ask for authorization before pushing.

For any new commit, use the configured Git identity and omit added `Co-authored-by` trailers. Preserve existing commits and their attribution.

## Resolve mechanical conflicts and ask about decisions

Identify the operation, its original commits and base, and every conflicted path. For an operation already in progress, use its recorded state. Do not treat a previously conflicted operation as conflict-free because its index is now resolved.

Establish each side's intent from the surrounding code and relevant history. Follow PR or issue links when intent remains unclear.

Label the sides with their actual branches or commits. During a rebase, `ours` is the rebased result so far and `theirs` is the commit being replayed.

A mechanical resolution preserves both sides' intent without choosing behavior. Resolve those first. Treat incompatible behavior, competing contracts, and missing intent as decisions for the user, whatever the file type.

Group related hunks into one decision. Before editing decision-dependent hunks, show the user:

- The affected files and the project behavior they control.
- Focused diffs for both sides, with base context where useful.
- What each changed part does, the available options, the recommended resolution, and its trade-off.

Apply decisions the user has already supplied. For the rest, ask and wait for an explicit answer before editing dependent hunks. Continue independent resolutions while waiting.

Preserve unrelated work. Once every conflicted path at the current stop is resolved, stage only the changes belonging to the operation.

## Check and delegate a review

Run the project's relevant checks against the resolved result.

Review the staged resolution before handing it back. State that the review covers only the resolved state reached so far, including when a rebase or cherry-pick has later steps remaining.

Delegate the review using the same provider, model, reasoning effort, and speed or service tier as the agent performing the merge, unless the user specifies different review settings. If the delegation tool cannot match or verify a setting, report that limitation rather than silently substituting.

Delegate one read-only reviewer, with no further delegation. Pass:

- The repository, original commits and base, and the resolved index or completed result.
- Both sides' intent, the user's decisions, and the checks performed.
- A request to find lost intent, incorrect resolutions, and incompatibilities between changes that merged cleanly.

When the `worth-doing` skill is available, apply it in both review roles and pass its accessible path to the reviewer.

Check findings independently against the code. Fix supported merge defects and rerun affected checks. Bring new behavior choices back to the user before editing them.

Allow at most one focused recheck for substantive fixes. If review cannot run, report the limitation and leave any still-open operation pending.

## Finish and report

For the conflict path, hand back the staged resolution after checks and review. If the user subsequently authorizes completing it, verify the current state and address any outstanding checks or findings first. Perform only the actions that instruction authorizes. In a rebase or cherry-pick sequence, pause again after resolving any new conflicts.

After a successful push, check the matching PR's actual state. GitHub can mark it merged when its head commits become reachable from its base through a normal merge or fast-forward. Report the observed state rather than assuming it closed. Do not rely on this detection after a local squash or rebase.

If the PR remains open, verify whether its current head is included in the pushed target. If it is included, tell the user and recommend closing the PR after verification. If it is not included, explain what remains unmerged. Never explicitly close a PR unless the user asks, and do not delete branches unless requested.

Read and apply the `unslop` skill to the report. If it is not in the available skills list, read `../unslop/SKILL.md` relative to this skill's directory. If neither exists, write in plain, direct language.

Report the source and target, operation state, commit and push status, check results and limitations, review outcome when applicable, and related PR status. For a pending operation, say what is staged and what instruction is needed to finish it.

End with an `After this merge` section. List concrete remaining checks or follow-ups the integration supports, including behavior, logic, or failures outside the conflicted files. For each item, name the affected behavior or path, explain the concern, and give the next check or action. If nothing further is warranted within the reviewed scope, say so.
