---
name: xlsx
description: Create, read, edit, repair, analyze, format, chart, or convert spreadsheet files when the primary input or deliverable is .xlsx, .xlsm, .csv, or .tsv. Use for template-preserving workbook edits, data cleanup, formulas, reporting, financial models, and spreadsheet format conversion. Do not use when the primary deliverable is a document, web page, standalone script, database pipeline, or live Google Sheets integration.
---

# Spreadsheet workflow

## Decide the deliverable

1. Inspect the source workbook, sheet names, used ranges, formulas, merged cells, tables, charts, validations, hidden rows or columns, and styles before editing.
2. Preserve established template conventions. Do not restyle an existing workbook unless requested.
3. Choose the implementation:
   - Use `pandas` for tabular analysis, cleanup, joins, reshaping, and CSV/TSV work.
   - Use `openpyxl` for workbook structure, formulas, formatting, charts, validations, and template-preserving edits.
   - Use both when data transformation and workbook presentation are required.
4. Save to a new output file unless the user explicitly asks to overwrite the source.
5. Reopen and verify the saved artifact. Recalculate formulas when formulas were added or changed.

## Preserve workbook integrity

- Keep formulas, styles, merged cells, row heights, column widths, print settings, freeze panes, filters, validations, comments, and hidden state unless the task requires changing them.
- For `.xlsm`, load and save with `keep_vba=True`. Do not claim that `openpyxl` preserves unsupported Excel features perfectly; verify critical macro-enabled files in Excel when possible.
- Never save a workbook opened with `data_only=True`; use it only for reading cached formula results.
- Treat identifiers, account numbers, postal codes, and similar fields as text when leading zeros matter.
- Handle dates, time zones, blanks, errors, and `NaN` explicitly.
- For large files, prefer `read_only=True`, `write_only=True`, or selected columns and sheets.

## Choose formulas or values intentionally

Use Excel formulas when the workbook is expected to remain dynamic, auditable, or user-editable. Use computed values when the output is a static export, cleaned dataset, snapshot, or interoperability file.

When writing formulas:

- Put reusable assumptions in dedicated cells and reference them.
- Guard expected edge cases such as division by zero.
- Verify relative and absolute references, cross-sheet references, and copied ranges.
- Test a few representative cells before filling large ranges.
- Avoid unintended circular references and external links.

Do not replace existing formulas with values unless requested.

## Formatting

- Match existing workbook styles first.
- For a new workbook, use a consistent professional font, readable headers, sensible widths, and number formats appropriate to the data.
- State units in headers where ambiguity is possible.
- Do not apply financial-model color conventions to ordinary spreadsheets.

For a new financial model, unless the user or template specifies otherwise:

- Blue font: editable hardcoded inputs.
- Black font: formulas.
- Green font: links to other worksheets in the same workbook.
- Red font: external workbook links.
- Yellow fill: assumptions requiring attention.
- Use parentheses for negatives, `0.0%` for percentages, `0.0x` for multiples, and formats that display zero as `-` when appropriate.
- Document material hardcoded assumptions with source, date, and reference.

## Formula recalculation and verification

`openpyxl` writes formulas but does not evaluate them. After adding or changing formulas, run:

```text
python scripts/recalc.py <workbook.xlsx> [timeout_seconds]
```

The script uses LibreOffice, recalculates the workbook, and reports formula errors. It supports Windows, Linux, and macOS when LibreOffice is installed or discoverable.

If LibreOffice is unavailable, preserve formulas, set workbook calculation mode to automatic when possible, and clearly report that cached values could not be refreshed. Do not claim formula correctness without verification.

Resolve all newly introduced `#REF!`, `#DIV/0!`, `#VALUE!`, `#NAME?`, `#NULL!`, `#NUM!`, and unexpected `#N/A` errors. Existing intentional errors should be reported rather than silently changed.

## Minimum verification checklist

- Confirm the output file opens successfully.
- Confirm expected sheets and dimensions.
- Compare key values, formulas, and styles with the source or task requirements.
- Check that identifiers and dates retained their intended types and display.
- Check formulas and cached results after recalculation.
- Confirm no unexpected external links, broken references, or lost macros.
- For important deliverables, visually inspect representative sheets in Excel or LibreOffice.

## Common patterns

```python
import pandas as pd

df = pd.read_excel("input.xlsx", dtype={"id": str})
df.to_excel("output.xlsx", index=False)
```

```python
from openpyxl import load_workbook

wb = load_workbook("input.xlsx")
ws = wb["Sheet1"]
ws["B10"] = "=SUM(B2:B9)"
wb.save("output.xlsx")
```

For macro-enabled workbooks:

```python
from openpyxl import load_workbook

wb = load_workbook("input.xlsm", keep_vba=True)
wb.save("output.xlsm")
```
