---
name: form-filling
description: Use when the user wants to fill in a PDF form with PDFBetter - read the fields of a fillable PDF, fill them from details the user gives, start from a saved template, or check responses to the user's published forms.
---

# Fill PDF forms

## Fill a fillable PDF

1. Get the document id (see the `pdf-tasks` skill if it isn't in the account yet). For a blank form the user saved as a template, use `list_templates` and `create_from_template` so the template itself stays blank.
2. Call `list_fields` to see each field's name, type, current value and allowed options.
3. Map the user's details to fields. Ask for anything required that the user hasn't given rather than inventing it: names, dates, ID numbers, amounts and signatures must come from the user. For checkboxes, radio groups and dropdowns, use one of the listed options exactly.
4. Call `fill_fields` with the values. It saves a new revision of the same document, and earlier revisions stay in its history.
5. Show the user what you filled, field by field, and offer a download with `export_document`.

If `list_fields` returns no fields, the PDF isn't fillable. Say so, and suggest opening it in the PDFBetter editor at https://pdfbetter.com/ to add fields or type on the page.

## Published forms

- `list_forms` lists the user's published fillable forms.
- `list_form_responses` returns the answers people submitted to a form.
- `list_form_submissions` shows recent submissions (which form, when, respondent email when the form asked for one) without the answers.

Treat respondents' answers as personal data: summarize what the user asks for, and don't repeat more of it than they need.
