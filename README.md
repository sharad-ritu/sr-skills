# sr-skills

Reusable agent skills by Sharad for Claude Code, Codex, and other coding agents.

## Skills

| Skill | Say | What it does |
| --- | --- | --- |
| [just-asking](skills/just-asking/SKILL.md) | "just asking" | Answers concisely in chat without changing files. Puts material related considerations after the main answer. |
| [worth-doing](skills/worth-doing/SKILL.md) | "worth doing" | Filters review findings and improvement suggestions by evidence, current benefit, cost, and scope. Works for reviewers and agents assessing their feedback. |
| [guided-merge](skills/guided-merge/SKILL.md) | `/guided-merge` | Resolves mechanical conflicts, asks about behavior choices before editing, delegates a review, and lists remaining checks. |
| [write-doc](skills/write-doc/SKILL.md) | `/write-doc` | Creates Markdown or light-theme HTML documents organized for their purpose, with necessary context, sources, and useful visuals. |

The agent can select `just-asking` and `worth-doing` from ordinary language. `guided-merge` and `write-doc` run only when invoked by name:

| Agent | Invoke |
| --- | --- |
| Claude Code | `/just-asking How does auth work?` |
| Codex | `$just-asking How does auth work?` |

The skills apply the [`unslop`](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop) skill to their output when it is installed. If it is missing, they answer in plain language.

### just-asking

```text
Just asking, how does authentication work in this repo?
```

```text
/just-asking How does authentication work in this repo?
```

Read-only investigation is allowed. Code snippets, diagrams, and HTML visuals stay in chat. T3 Code's HTML rendering tools are optional. It can use other available skills when relevant, while keeping the work read-only.

### worth-doing

Use it for a direct review, suggestions, or a delegated review:

```text
Review this feature using worth-doing.
```

```text
Suggest improvements to this module using worth-doing.
```

```text
Delegate a review using worth-doing. Pass the skill to the reviewer
and independently assess its recommendations before acting.
```

Its decisions are `Do now`, `Follow up`, `Investigate`, and `Omit`. It filters out unsupported or low-value suggestions before reporting. It does not require a particular model or authorize fixes or delegation by itself.

### guided-merge

Invoke it during a conflicted merge, rebase, or cherry-pick:

```text
/guided-merge
```

```text
/guided-merge Finish this rebase.
```

Mechanical resolutions proceed directly. Behavior choices reach you with project context, focused diffs, and a recommendation before any edits.

By default it leaves the resolution staged after checks and a delegated review. An instruction to finish the operation authorizes committing or continuing. For a full rebase, the review covers the completed series. The final `After this merge` section lists specific remaining checks and follow-ups.

### write-doc

Invoke it with the document you need:

```text
/write-doc Write a Markdown proposal for the improvement we discussed.
```

```text
/write-doc Summarize this research as HTML for product and engineering readers.
```

It infers the purpose and audience from context, and asks when missing information would materially change the document. Markdown is the default. HTML uses a self-contained light theme, with interaction when it helps the reader.

It follows the project's document locations, otherwise saving under `docs/` in a project or the current directory outside one. You can specify the format and destination in your request.

### Combining them

Combine the skills to keep a review in chat:

```text
Just asking: delegate a review of this feature using worth-doing.
Report worthwhile recommendations without making changes.
```

## Install

You need [Node.js](https://nodejs.org) 22.20 or later for `npx`. The [`skills`](https://www.npmjs.com/package/skills) installer supports Claude Code, Codex, Cursor, and other coding agents.

Install all skills for your user account:

```bash
npx skills add sharad-ritu/sr-skills --skill '*' -g
```

Choose your coding agents when prompted. To install only some skills, name each one:

```bash
npx skills add sharad-ritu/sr-skills -s just-asking -s worth-doing -g
```

Install [`unslop`](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop) too. The skills use it to keep their writing plain, and work without it:

```bash
npx skills add cursor/plugins --skill unslop -g
```

Leave out `-g` to install into the current project instead. Start a new agent session if the skills do not appear.

### Update or remove

```bash
npx skills update -g
npx skills remove guided-merge -g
```

The installer keeps one copy of each skill in `~/.agents/skills` and links each agent to it.

### Install without npx

Copy a skill folder from [`skills/`](skills) into your agent's skills directory:

- Claude Code reads `~/.claude/skills/<name>/`.
- Codex reads `~/.agents/skills/<name>/`.

Keep the folder name equal to the skill's `name`, and keep `unslop` beside the other skills so they can find it.

### Contribute

Each skill lives in `skills/<name>/SKILL.md`, with optional `references/` and Codex metadata in `agents/openai.yaml`. Test a local change with:

```bash
npx skills add . --skill '*' -g
```

## References

The skill structure and writing draw on [pstack](https://github.com/cursor/plugins/tree/main/pstack), [Matt Pocock's skills](https://github.com/mattpocock/skills), and [Theo's tstack](https://github.com/t3dotgg/tstack). Theo's [video on his skill workflow](https://www.youtube.com/watch?v=5Bmp9cz1JN8) explains the natural-language triggers and explicit stopping points used here. `just-asking` is tailored to chat-only requests.

`worth-doing` also draws on [sol-loop](https://github.com/t3dotgg/tstack/blob/main/skills/sol-loop/SKILL.md) for scope control, minimal changes, independent assessment, and bounded review rounds. It applies those ideas to both fixes and improvements without requiring Sol or a review loop.

`write-doc` draws on [Karpathy's post about understanding model outputs](https://x.com/karpathy/status/2105819303471976479) for controlled-language writing, diagrams, and interactive HTML.
