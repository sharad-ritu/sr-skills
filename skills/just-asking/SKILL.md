---
name: just-asking
description: "Answer in chat without changes. Use when the user says 'just asking' or 'just-asking' as an instruction, or requests discussion or an explanation only. Requests to create or edit this skill are not invocations."
---

# Just asking

Answer the question in chat, then stop. Recommendations are not permission to implement them.

## Keep the work in chat

Use read-only tools to inspect files, search sources, and check facts. Cite the files or sources the answer relies on.

Do not edit code, create files or documents, install dependencies, or change local or external state. This includes commands and tests that write artifacts. Show proposed code or commands as snippets, without running or saving them.

Interpret the user's intent, not just the trigger words. A quoted example of the phrase does not activate this skill. This scope applies to the current request. A later explicit request to make changes can authorize action.

## Use the relevant skills

Read and apply the `unslop` skill before sending the answer. If it is not in the available skills list, read `../unslop/SKILL.md` relative to this skill's directory. If neither exists, say so briefly and use plain, direct language without installing anything.

Use other available skills only when they help answer this question. Keep their work read-only and their output in chat, even if they normally create artifacts. A delegated agent does not inherit this skill, so state the read-only and chat-only limits in its brief.

## Answer the main question first

- Lead with the direct answer to the user's question, not an inventory of your investigation. Add only the explanation and evidence needed to understand it.
- Use short paragraphs, bullets, or a compact table.
- Put missing context, consequences, or effects on related systems under a separate `Related considerations` heading after the main answer. Include only points that could change the user's understanding or decision, and explain a risk without expanding the question into an audit. Omit the section otherwise.

## Show examples and visuals inline

Use code snippets, diagrams, or inline HTML when they explain the answer more clearly than prose. Use Mermaid when the client supports it, or text diagrams otherwise. Simple answers need no visual.

In T3 Code, render inline HTML with the `html_preview` and `html_render` tools. Where they are unavailable, use Markdown, snippets, or text diagrams. Claim a rendered result only after `html_render` succeeds.
