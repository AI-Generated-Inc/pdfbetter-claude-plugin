---
name: data-extraction
description: Use when the user wants structured data pulled out of PDFs in PDFBetter - invoice totals, contract dates, bank statement lines, form answers - from one document or many, reviewed and exported as JSON, CSV or Excel.
---

# Extract data from PDFs

PDFBetter extracts fields with page numbers and a verbatim quote for every value, and marks each value's status. Never invent a value the tool marked as missing.

## 1. Decide the fields

- Check for a saved schema first: `list_extraction_schemas`.
- If none fits, either pass inline field definitions to `extract_document`, or save a reusable schema with `create_extraction_schema` when the user will run the same extraction again. Field types: text, number, date, boolean, currency, enum (with options) and table (with columns). Keep names short and specific, such as `invoice_total` or `due_date`.

## 2. Run it

- **One document:** `extract_document` with `schemaId` or inline fields. Long documents start a batch automatically.
- **Many documents:** `start_extraction_batch` with the document ids, then poll `get_extraction_batch` until it finishes. Failures are isolated per document, so report which ones failed instead of treating the whole batch as failed.

## 3. Report values honestly

Each value has a status:

- `found`: verified against the page text. Report it with its page.
- `unverified`: a value was read but the quote didn't match exactly. Show it and ask the user to check it.
- `missing`: not in the document. Say so; don't guess.
- `invalid`: didn't match the field type. Show what was read.

If the user corrects values or rejects a run, record it with `review_extraction`. Corrected values are what exports use.

## 4. Export

`export_extraction` with `format` `json`, `csv` or `xlsx` and a `batchId` or `runIds`. It returns a download link valid for 15 minutes. Rejected runs are left out, and CSV with table fields comes as a zip.

Extraction uses 1 AI credit per page read. If credits run out, tell the user and point to https://pdfbetter.com/pricing/.
