# PDF Document Processing Pipeline

Accepts a PDF upload via webhook and runs a multi-stage processing pipeline: extracts text as Markdown, generates a summary table, converts back to HTML, and returns all three outputs combined. Useful for document intake, contract analysis, and report digestion.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `@acrewity/n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `@acrewity/n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Webhook** — Accepts a PDF file upload (binary)
2. **Extract Text as Markdown** — Converts the PDF to Markdown via Acrewity's `pdf_to_markdown`
3. **Generate Summary Table** — Produces a Markdown table summarizing key content via Acrewity's `markdown_table_generator`
4. **Convert to HTML** — Converts the Markdown to HTML via Acrewity's `markdown_to_html`
5. **Combine Results** — Merges all three outputs into one response object
6. **Return Processed Document** — Returns `{ markdown, summaryTable, html }`
