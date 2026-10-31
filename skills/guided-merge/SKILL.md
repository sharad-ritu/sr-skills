---
name: guided-merge
description: "Resolve merge conflicts with your input, a delegated review, and follow-up checks."
disable-model-invocation: true
---

# Guided merge

Follow this workflow instead of any other merge-conflict skill for this invocation.

## Establish the scope

Identify the operation (merge, rebase, or cherry-pick), its original source and target commits, its base, and every conflicted path. Keep the original commit IDs available for review.

Establish each side's intent from the surrounding code and relevant history. Follow PR or issue links when intent remains unclear.

Label the sides with their actual branches or commits. During a rebase, `ours` is the rebased result so far and `theirs` is the commit being replayed.

Default to leaving the resolution staged. Commit or continue the operation only when the user has already authorized completing it.

## Resolve mechanical conflicts and ask about decisions

A mechanical resolution preserves both sides' intent without choosing behavior. Resolve those first. Treat incompatible behavior, competing contracts, and missing intent as decisions for the user, whatever the file type.

Group related hunks into one decision. Before editing decision-dependent hunks, show the user:

- The affected files and the project behavior they control.
- Focused diffs for both sides, with base context where useful.
- What each changed part does, the proposed resolution, and its trade-off.

Apply decisions the user has already supplied. For the rest, ask and wait for an explicit answer.

Preserve unrelated work. Once every conflicted path at the current stop is resolved, stage only the changes belonging to the operation.

When completing a rebase or cherry-pick sequence is authorized, continue through its stops using the same decision process.

## Check and delegate a review

Run the project's relevant checks against the resolved result.

Review a merge before committing it. For an authorized rebase or cherry-pick sequence, review the complete result once the sequence finishes. When stopping staged, state that the review covers only the resolved state reached so far.

Delegate one read-only reviewer, with no further delegation. Pass:

- The repository, original commits and base, and the resolved index or completed result.
- Both sides' intent, the user's decisions, and the checks performed.
- A request to find lost intent, incorrect resolutions, and incompatibilities between changes that merged cleanly.

When the `worth-doing` skill is available, apply it in both review roles and pass its accessible path to the reviewer.

Check findings independently against the code. Fix supported merge defects and rerun affected checks. Bring new behavior choices back to the user before editing them.

Allow at most one focused recheck for substantive fixes. If review cannot run, report the limitation and leave any still-open operation pending.

## Finish and report

Finish an authorized operation after addressing supported review findings.

Read and apply the `unslop` skill to the report. If it is not in the available skills list, read `../unslop/SKILL.md` relative to this skill's directory. If neither exists, write in plain, direct language.

Report the resolution, operation state, check results and limitations, and review outcome.

End with an `After this merge` section. List concrete remaining checks or follow-ups the integration supports, including behavior, logic, or failures outside the conflicted files. For each item, name the affected behavior or path, explain the concern, and give the next check or action. If nothing further is warranted within the reviewed scope, say so.
