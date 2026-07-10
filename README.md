# Acrewity n8n Workflow Templates

Ready-to-import n8n workflows powered by the [Acrewity API](https://acrewity.com) — a verified n8n community node with 22 utility services for documents, QR codes, Excel files, web content, and more.

## Quick start

1. In n8n go to **Settings > Community Nodes** and install `@acrewity/n8n-nodes-acrewity` (verified by n8n, also installable directly from the n8n interface)
2. Get a free API key at [acrewity.com](https://acrewity.com) (100 free credits/month)
3. Open a workflow folder below and import its `workflow.json` via **Workflows > Import from file**
4. Add your Acrewity credential under **Credentials > New > Acrewity API**

## Workflows

Complete automations you can run as-is: a real trigger, the work, and delivery of the result.

| Workflow | What it automates | Integrations |
|---|---|---|
| [Daily Website Monitor](workflows/daily-website-monitor/) | Watches a list of URLs daily and emails you a digest of what changed | Schedule, `url_to_markdown`, `text_diff`, email |
| [HTML Invoice to PDF Email](workflows/html-invoice-to-pdf-email/) | Converts an HTML invoice to PDF and sends it to the customer as an email attachment | `html_to_pdf`, SMTP |
| [Acrewity AI Agent](workflows/acrewity-ai-agent/) | Natural-language interface to all 22 services — the AI picks the right tool automatically | AI Agent, Claude, all services |

More end-to-end workflows are on the way, starting with a Google Sheets order-to-invoice pipeline (Sheets trigger, PDF invoice, Gmail delivery, Drive archive).

## Building blocks

Minimal single-service examples. Not full automations — use them to see how each Acrewity service is called, then drop the pattern into your own workflow.

| Example | Service(s) |
|---|---|
| [Contact vCard QR](examples/contact-vcard-qr/) | `qr_code_generator` |
| [Excel Upload to JSON](examples/excel-upload-to-json/) | `excel_to_json` |
| [JSON Payload Validator](examples/json-payload-validator/) | `json_schema_validator` |
| [JSON to Excel & Email](examples/json-to-excel-email/) | `json_to_excel`, `email_access` |
| [PDF Processing Pipeline](examples/pdf-processing-pipeline/) | `pdf_to_markdown`, `markdown_table_generator`, `markdown_to_html` |
| [QR Codes for E-commerce](examples/qr-codes-for-ecommerce/) | `qr_code_generator` |
| [SEO Page Analyzer](examples/seo-page-analyzer/) | `url_to_markdown` + Claude |
| [URL Content Diff](examples/url-content-diff/) | `url_to_markdown`, `text_diff` |
| [URL to Markdown LLM Pipeline](examples/url-to-markdown-llm-pipeline/) | `url_to_markdown` + Claude |
| [Web Page AI Summarizer](examples/web-page-ai-summarizer/) | `url_to_markdown` + Claude |

## About Acrewity

[Acrewity](https://acrewity.com) is an API platform with 22 utility services for document generation, file conversion, QR codes, web scraping, email, and more. Install the community node once, access everything.

```
npm install @acrewity/n8n-nodes-acrewity
```

Or install via **Settings > Community Nodes** in n8n using the package name `@acrewity/n8n-nodes-acrewity`.

Free plan includes 100 credits/month. Each API call costs 1 credit.

## Contributing

Found a bug or want to improve a workflow? Open an issue or submit a pull request.
