---
name: pdf-tasks
description: Use when the user wants to do something with a PDF through PDFBetter - bring a document in, then merge, split, rotate, extract pages, convert to or from Word/Excel/PowerPoint/images, compress, or OCR a scan. Covers finding documents, uploading, long-running jobs and download links.
---

# PDF tasks with PDFBetter

PDFBetter works on documents stored in the user's PDFBetter account. Every tool takes document ids, so the first step is always to get the document into the account and know its id.

## 1. Get the document

- **Already in the account:** call `list_documents` (pass `query` to match a title or tag when the user names one) and confirm which document they mean when more than one matches.
- **Public link:** call `create_document_from_url` with the URL.
- **Local file** (Claude Code or a session that can run commands): call `create_upload` with the exact file name, size in bytes and MIME type, `PUT` the bytes to the returned `url` with the returned headers within 10 minutes, then call `create_document_from_upload` for a PDF, or `convert` with `uploadIds` and `to: "pdf"` for Word, Excel, PowerPoint or text.
- **Start from a template:** `list_templates`, then `create_from_template`.

## 2. Pick the tool

| The user wants to | Tool |
| --- | --- |
| Combine PDFs | `merge_documents` |
| Split by page ranges, every N pages, or one file per page | `split_document` |
| Keep only some pages | `extract_pages` |
| Rotate pages | `rotate_pages` |
| Convert (PDF to Word, Excel, PowerPoint, JPG, text, CSV, or Office to PDF) | `convert` |
| Make the file smaller | `compress_document` |
| Make a scan searchable | `ocr_document` |
| Download the current version | `export_document` |

## 3. Handle results

- Page operations and templates create a **new** document; the original is never changed. `fill_fields` and `ocr_document` save a new revision of the same document, and earlier revisions stay in its history. Tell the user which happened.
- Conversions, compression and large OCR return a job id. Poll `get_job` until the status is `succeeded` or `failed`, then share the download link it returns. Don't start the same conversion again while a job is running.
- Download links expire after a few minutes. If the user asks for the file later, call `export_document` or `get_job` again for a fresh link.

## 4. Limits

Each tool call and the work it triggers count against the monthly allowances of the user's PDFBetter plan. If a tool reports that an allowance ran out, say which one and point to https://pdfbetter.com/pricing/ instead of retrying. For questions about PDFBetter itself (settings, plans, why something failed), use `search_help` and `get_help_article` and cite the article link.
