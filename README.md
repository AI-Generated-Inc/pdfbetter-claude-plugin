# PDFBetter for Claude

PDFBetter is an AI-native PDF editor for forms, e-signatures and documents. This plugin connects Claude to the PDFs in your PDFBetter account and teaches Claude how to use them well: answers and summaries that cite their pages, merging, splitting, converting, compressing and OCR, filling forms, extracting data into spreadsheets, and comparing two versions of a contract.

It works in Claude chat, Cowork and Claude Code.

## What's inside

- **MCP connector** `pdfbetter`: the remote PDFBetter server at `https://pdfbetter.com/api/mcp/`. You sign in to PDFBetter and approve access the first time Claude uses it. No API key is stored in this plugin.
- **Skills**
  - `pdf-tasks`: bring a document in (from your account, a public link or a local file), then merge, split, rotate, extract pages, convert, compress or OCR it, and handle long-running jobs and download links.
  - `document-answers`: ask questions, summarize, build a mind map or a brief across several documents, compare versions (facts first, interpretation labeled), and find personal data to review for redaction.
  - `data-extraction`: pull fields such as totals, dates and line items from one or many PDFs, report each value with its page and status, and export JSON, CSV or Excel.
  - `form-filling`: read a fillable PDF's fields, fill them from your details, start from a saved template, and read responses to your published forms.

## Getting started

1. Install the plugin from the Claude directory.
2. Ask Claude something like "Summarize the lease in my PDFBetter account" or "Merge these two PDFs".
3. When Claude first calls PDFBetter, sign in (or create a free account) and select **Allow and connect**.

To disconnect, open PDFBetter **Settings** → **Agents (MCP)** and revoke the key named **Claude**. Full setup notes: https://help.pdfbetter.com/automation/connect-ai-agents-mcp/

## What the plugin sends and where

The plugin contains no code that runs on your computer. Claude calls only the PDFBetter server above, and only when you ask for something that needs it. Each call sends the tool's inputs (for example a document id, a question, field values, or a public URL you gave Claude) to PDFBetter, which processes your documents in your account. Results come back as text, new documents or revisions, and short-lived download links. Original documents are never overwritten.

Each tool call and the work it triggers count against the monthly allowances of your PDFBetter plan. AI features use AI credits. Plans and limits: https://pdfbetter.com/pricing/

## Privacy and terms

- Privacy policy: https://pdfbetter.com/privacy/
- Terms of service: https://pdfbetter.com/terms/

## Support

Help center: https://help.pdfbetter.com/ · Contact: support@pdfbetter.com

PDFBetter is operated by AI Generated Inc.
