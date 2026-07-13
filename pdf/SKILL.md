---
name: pdf
description: Read, extract, OCR, create, merge, split, rotate, watermark, fill, encrypt, decrypt, inspect, render, and verify PDF files. Use whenever a PDF is the primary input or deliverable, including scanned documents, forms, tables, images, and layout-sensitive reports.
---

# PDF workflow

Choose the tool according to whether the task concerns content, page structure, forms, or visual layout. Read [reference.md](reference.md) for advanced libraries and troubleshooting. Read [forms.md](forms.md) before filling or modifying PDF forms.

## Inspect first

1. Determine whether the PDF is text-based, scanned, encrypted, malformed, or form-enabled.
2. Record page count, page sizes, rotation, metadata, bookmarks, attachments, and form fields relevant to the task.
3. Render representative pages before editing when layout matters.

## Choose the tool

- Use `pypdf` for merge, split, rotate, metadata, encryption, and basic page operations.
- Use `pdfplumber` for text and table extraction with layout awareness.
- Use Poppler tools for fast text extraction, image extraction, metadata, and page rendering.
- Use OCR only for scanned or image-only pages; preserve the original visual layer when adding searchable text.
- Use ReportLab for generated PDFs, with explicit page size, margins, fonts, and pagination.
- Use the form workflow in `forms.md` for AcroForm or XFA documents.

## Preserve and protect

- Save to a new file unless overwrite is explicitly requested.
- Preserve page order, dimensions, rotation, bookmarks, metadata, links, annotations, forms, and accessibility information unless the task changes them.
- Never remove encryption or bypass access controls without authorization and a supplied credential.
- Avoid rasterizing vector or text content unless required.
- Embed fonts needed for non-Latin text and verify glyph coverage.
- Do not use Unicode subscript or superscript glyphs with ReportLab built-in fonts; use markup or embedded fonts.

## Verify every deliverable

1. Reopen the output with an independent parser.
2. Confirm page count, sizes, rotation, and expected metadata or fields.
3. Extract text from representative pages and compare with expected content.
4. Render all changed pages to images and inspect clipping, overlap, missing glyphs, low resolution, and incorrect orientation.
5. Confirm forms, links, bookmarks, encryption, and OCR searchability when relevant.

For large PDFs, test a small representative page range before processing the whole file. If a dependency or visual verification tool is unavailable, report the unverified aspect explicitly.
