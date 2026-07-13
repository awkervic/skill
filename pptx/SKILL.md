---
name: pptx
description: Create, read, edit, combine, split, restyle, render, and visually verify PowerPoint .pptx presentations. Use for slide decks, pitch decks, templates, layouts, speaker notes, comments, charts, images, and text extraction whenever a presentation is an input or deliverable.
---

# PPTX workflow

Preserve template semantics when editing and use a render-inspect-fix loop for every delivered deck.

Read [editing.md](editing.md) before editing or creating from a template. Read [pptxgenjs.md](pptxgenjs.md) before creating a deck from scratch. Read [design-and-qa.md](design-and-qa.md) when choosing visual direction or diagnosing layout issues.

## Inspect

1. Extract text and speaker notes.
2. Generate a thumbnail overview.
3. Inspect slide size, masters, layouts, theme fonts and colors, placeholders, charts, media, links, comments, and hidden slides.
4. Identify the slides and shared resources affected by the task.

Useful commands:

```text
python -m markitdown input.pptx
python scripts/thumbnail.py input.pptx
python scripts/office/unpack.py input.pptx unpacked/
```

## Edit or create

- Match the existing theme, layouts, spacing, and visual language when editing a template.
- Use the smallest set of slide and master changes needed.
- Preserve notes, comments, hyperlinks, animations, embedded media, and hidden state unless explicitly changing them.
- For a new deck, establish a content hierarchy, grid, palette, typography, and visual motif appropriate to the audience and subject.
- Prefer diagrams, charts, images, and meaningful spatial structure when they improve understanding; do not add decoration without purpose.
- Vary layouts only enough to support the content while keeping the deck coherent.
- Keep text readable, margins consistent, and sources visible without colliding with content.

## Verify

1. Extract text from the output and check omissions, ordering, spelling, and leftover placeholders.
2. Render the deck to PDF and slide images.
3. Inspect every slide for overflow, overlap, clipping, low contrast, poor alignment, inconsistent spacing, missing media, and broken charts or fonts.
4. Fix issues and rerender affected slides.
5. Complete at least one full final pass after the last fix.

```text
python scripts/office/soffice.py --headless --convert-to pdf output.pptx
pdftoppm -jpeg -r 150 output.pdf slide
```

Do not claim visual correctness from source code alone. If rendering dependencies are unavailable, report that limitation explicitly.
