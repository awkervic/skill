---
name: docx
description: Create, read, edit, redline, comment on, convert, and visually verify Microsoft Word .docx files. Use for reports, letters, memos, templates, formatting, tables, images, headers, footers, tracked changes, comments, content extraction, and legacy .doc conversion when the primary artifact is a Word document.
---

# DOCX workflow

Treat a DOCX as both a document and an OOXML package. Preserve semantics and layout, then render and inspect the result.

Read [reference.md](reference.md) when creating complex documents, editing OOXML, adding tracked changes or comments, or troubleshooting package structure.

## Choose the path

- Read or extract content: use `pandoc --track-changes=all` or unpack OOXML when structure matters.
- Create a new document: use `docx-js` for structured layouts and reusable styles.
- Edit an existing document: preserve the source by unpacking, making surgical XML changes, repacking, and validating.
- Convert legacy `.doc`: use LibreOffice before editing.
- Accept tracked changes: use `scripts/accept_changes.py`.

## Edit safely

1. Inspect document structure, styles, sections, headers, footers, relationships, comments, and tracked changes.
2. Save to a new output file unless overwrite is explicitly requested.
3. Preserve existing styles, numbering, page setup, fields, relationships, and metadata unless the task requires changes.
4. Make the smallest XML or content change that satisfies the request.
5. Validate package structure.
6. Render to PDF or page images and visually inspect every affected page.

Use these bundled commands:

```text
python scripts/office/unpack.py input.docx unpacked/
python scripts/office/pack.py unpacked/ output.docx --original input.docx
python scripts/office/validate.py output.docx
```

## Creation requirements

- Set paper size and margins explicitly.
- Define reusable styles and use real heading levels.
- Use numbering definitions for bullets and numbered lists.
- Specify table and cell widths consistently.
- Put page breaks inside paragraphs.
- Specify image type and useful alternative text.
- Use headers, footers, fields, bookmarks, and hyperlinks structurally rather than simulating them with plain text.

## Tracked changes and comments

- Preserve original author metadata unless the user requests a specific author for new changes.
- Keep insertions and deletions as siblings of runs; do not place change elements inside a run.
- Preserve run properties when replacing text.
- Mark paragraph deletion when removing an entire paragraph.
- Add comment relationships and markers using the bundled comment helper.
- Validate after every structural OOXML edit.

## Visual verification

Convert the final DOCX to PDF and render pages to images. Check page breaks, clipping, table overflow, headers and footers, numbering, image placement, tracked-change display, and unexpected blank pages. Iterate until the affected pages are clean.

If LibreOffice, Pandoc, Poppler, Node.js, or another required dependency is unavailable, report the missing verification step explicitly rather than claiming completion.
