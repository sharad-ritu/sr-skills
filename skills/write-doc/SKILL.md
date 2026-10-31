---
name: write-doc
description: "Create clear Markdown or light-theme HTML documents with the context and sources readers need."
disable-model-invocation: true
---

# Write a document

Create one document that serves the user's purpose. Keep proposed work as document content unless implementation is also requested.

Read and apply the `unslop` skill to the document and final response. If it is not in the available skills list, read `../unslop/SKILL.md` relative to this skill's directory. If neither exists, write in plain, direct language.

## Establish the brief, format, and destination

Before drafting, be able to state the subject, intended readers, and purpose. Identify what readers should be able to decide or do afterward. Infer the brief from the request and available context. Default to readers with mixed technical backgrounds.

Ask a focused question when missing information or competing interpretations would materially change the document. Otherwise proceed, making consequential assumptions visible.

Honor an explicit format or filename extension. Otherwise default to Markdown. Choose HTML when visual layout or interaction would materially improve understanding.

Follow applicable project templates. If none apply, follow the structure of similar documents.

For HTML, read and apply [HTML documents](references/html.md).

For Markdown, use ordinary headings, lists, tables, and links. Use Mermaid when the intended renderer supports it. Otherwise use a text diagram or table. Explain the diagram's takeaway in nearby prose.

Choose the destination before drafting. Use the requested destination. Otherwise follow the project's convention for similar documents. If none exists, use `docs/<topic>.md` or `docs/<topic>.html` under the project root. Outside a project, use the current directory.

For a new document, choose an unused descriptive filename. Update an existing document when the request is a revision.

## Establish the evidence

Use supplied material first. Inspect relevant repository files and linked sources before citing them. Research missing evidence when it affects the document's conclusions or requested decisions.

Cite material factual claims, measurements, and quotations near the text they support. Prefer primary sources for external facts. Give changing claims their relevant date, version, or environment.

Use descriptive Markdown links or HTML links. For repository evidence, use paths relative to the saved document, with a symbol, heading, line, or revision when needed to locate the evidence.

Distinguish observed facts, reported claims, inferences, and proposals. Treat missing owners, dates, estimates, and statuses as unknown.

When a source is unavailable, identify the affected claim and its uncertainty. If missing evidence prevents the intended conclusion, label the document as a draft and name what remains to establish.

## Compose for the reader

For R&D, proposals, research, bug lists, task lists, questions, or explanations, read [Document shapes](references/document-shapes.md) and use the closest row. For another purpose, organize around the reader's intended decision, action, or understanding.

Open with a short summary suited to the document's purpose, unless the template sets the opening. Follow with the context needed to understand it. Define essential technical terms on first use, and place specialist detail after the shared explanation.

Write about 80% of the way to ASD-STE100 Simplified Technical English: one instruction per sentence, short noun groups, and vertical lists for complex text. Review instructions over about 20 words, explanations over about 25 words, and paragraphs over four sentences. Use these limits as editing prompts and keep the phrasing natural.

When a passage is hard to follow, try a table, diagram, image, or concrete example before adding more prose. Give informative visuals a caption or nearby explanation, and attribute sourced images.

## Save and verify

Save the document, then reopen the saved artifact. Check it against the user's explicit requirements, any project template, the selected document shape, and any format-specific checks. Check local links and anchors from the document's location.

Cold-read it without relying on the conversation. A reader must be able to identify the purpose, understand the main point, and find the intended decision, action, or unresolved question.

Finish when these checks pass. Return a link to the document and state any consequential uncertainty or verification limitation.
