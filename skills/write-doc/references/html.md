# HTML documents

## Package one portable document

Produce one HTML file with inline CSS. Embed diagrams as SVG and included raster images as data URLs. Use inline JavaScript only when an interaction needs it.

Keep rendering independent of network requests, external libraries, fonts, and CDNs. External source links remain ordinary links.

Include the document language, UTF-8 charset, viewport metadata, and a meaningful page title. Use semantic headings, sections, lists, tables, and controls. Escape code and quoted material so it remains text.

## Design for reading

Declare `color-scheme: light`. Use a white or pale neutral background, dark text, and a restrained accent chosen for the subject. Keep body text contrast at least 4.5:1. Give links a visible treatment beyond color.

Use a readable system font stack. Set body text near 18px using rem units, with line height around 1.6. Give headings a clear hierarchy without making the opening resemble a promotional landing page.

Keep prose near 70 characters per line and left aligned. Use whitespace and headings as the main structure. Give wide tables and diagrams additional room only when needed.

On narrow screens, reflow the document. Let an oversized table scroll within its own region rather than widening the page.

Use callouts for information that changes interpretation or action, such as a decision, limitation, or risk. Give each a descriptive label and a quiet border or background.

## Make tables and visuals understandable

Give tables clear headers and units. Use header cells with the appropriate scope. Align comparable numbers consistently, and express status in text as well as color.

Give SVG diagrams a responsive `viewBox`, readable labels, and an accessible title and description. Explain their main point in nearby text. Provide underlying values in text or a table when readers need them to assess a chart.

## Add interaction for a reading task

Start with a static document. Add an interaction when it answers a concrete question, such as comparing assumptions, filtering a long issue list, or opening supporting detail.

Prefer native controls such as `details`, labeled inputs, and buttons. Use keyboard access and visible focus. Keep essential conclusions, evidence, and actions readable with JavaScript disabled.

For calculations, show the inputs, units, assumptions, and method. Identify illustrative data. Keep the underlying information available when filters or disclosures change what is visible.

Keep interaction within the document unless the user requests external actions.

## Support print

Add print styles with a white background and dark text. Hide controls while preserving their information. Expand supporting disclosures and include filtered-out records.

Make tables and diagrams fit the printed width. Keep headings with the content they introduce, and avoid clipped scroll regions. Preserve usable source references, including external destinations.

## Verify the saved file

When a renderer is available, open the saved file and inspect a wide and narrow viewport. Check the light theme, readable text, tables, diagrams, links, and overflow.

Exercise each interaction by keyboard. Check essential content with JavaScript disabled and inspect print output.

Correct observed problems before the final response. If a renderer or check is unavailable, state which verification remains unperformed.
