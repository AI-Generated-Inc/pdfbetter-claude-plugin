---
name: document-answers
description: Use when the user asks a question about a PDF in PDFBetter, wants a summary, a mind map or a brief, wants to compare two versions of a contract or document, or wants personal data found for redaction. Keeps page citations and separates what the document says from interpretation.
---

# Answers from documents, with citations

PDFBetter's AI tools read the document and cite the pages they used. Your job is to keep those citations visible and never present uncited claims as coming from the document.

## Questions and summaries

- **One question:** `ask_document` with the document id and the question. It only keeps quotes verified word for word against the page text, and says when the document doesn't contain the answer. When it says that, tell the user plainly; don't fill the gap from general knowledge without saying so.
- **Summary:** `summarize_document`. Keep the page references in your reply, for example "(p. 4)".
- **Mind map of the structure:** `mind_map_document`.
- **Several documents at once:** put them in a workspace (`create_workspace`, `add_to_workspace`), then `ask_workspace` for cross-document questions or `generate_brief` for a written brief. `list_workspace_outputs` shows earlier results.

## Comparing versions

`compare_documents` takes `originalId` and `revisedId`, or two revisions of one document. It returns two parts; report them separately:

1. **Facts:** verbatim before and after excerpts with page numbers, and changed amounts, dates and durations. Lead with these.
2. **Interpretation:** an AI grouping of the changes with a low, medium or high materiality hint. Label it as interpretation, and say it is not legal advice.

## Finding personal data

`suggest_redactions` lists sensitive text with page numbers. It never changes the document, and suggestions can miss things. Present them as a review list. Applying redaction removes content permanently, so it stays a human step in the PDFBetter app (AI redaction review or the editor); give the user that next step instead of claiming the document is redacted.

## Credits

Summaries, answers, interpretations and AI redaction categories use AI credits from the user's plan. If credits run out, the tool says so: tell the user and point to https://pdfbetter.com/pricing/ rather than retrying.
