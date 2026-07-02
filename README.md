# Acrewity n8n Workflow Templates

Ready-to-import n8n workflows powered by the [Acrewity API](https://acrewity.com). Automate documents, QR codes, Excel files, web monitoring, and more — no server setup required.

## Quick start

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Get a free API key at [acrewity.com](https://acrewity.com) (100 credits/month free)
3. Browse the workflows below, open the folder, and import `workflow.json` via **Workflows > Import from file**
4. Add your Acrewity credential under **Credentials > New > Acrewity API**

## Workflows

| Workflow | Description | Acrewity services used |
|---|---|---|
| [Invoice PDF Generator](workflows/invoice-pdf-generator/) | POST order data, receive a branded PDF invoice | `html_to_pdf` |
| [PDF Document Generator](workflows/pdf-document-generator/) | Generate invoices, quotes, receipts, estimates, and proformas from one endpoint | `html_to_pdf` |
| [HTML to PDF Invoice](workflows/html-to-pdf-invoice/) | Minimal demo — convert any HTML string to a PDF | `html_to_pdf` |
| [QR Code Generator](workflows/qr-code-generator/) | Generate a QR code image from any text or URL | `qr_code_generator` |
| [Contact vCard QR](workflows/contact-vcard-qr/) | POST contact info, receive a scannable QR code that adds to phone contacts | `qr_code_generator` |
| [URL to Markdown](workflows/url-to-markdown/) | Fetch any web page and get back clean Markdown | `url_to_markdown` |
| [URL Content Diff](workflows/url-content-diff/) | Compare two web pages and see what changed | `url_to_markdown`, `text_diff` |
| [JSON to Excel & Email](workflows/json-to-excel-email/) | Convert a JSON array to an Excel file and email it | `json_to_excel`, `email_access` |
| [Web Page AI Summarizer](workflows/web-page-ai-summarizer/) | Fetch a page, extract text, return an AI-generated summary | `url_to_markdown` + Claude |
| [Daily Website Monitor](workflows/daily-website-monitor/) | Detect changes on a list of URLs and send email alerts | `url_to_markdown`, `text_diff`, `email_access` |
| [SEO Page Analyzer](workflows/seo-page-analyzer/) | Get a full SEO report for any URL — keywords, headings, score, recommendations | `url_to_markdown` + Claude |
| [PDF Processing Pipeline](workflows/pdf-processing-pipeline/) | Upload a PDF, extract Markdown, generate summary table, convert to HTML | `pdf_to_markdown`, `markdown_table_generator`, `markdown_to_html` |
| [Markdown Table Generator](workflows/markdown-table-generator/) | Convert a JSON array to a formatted Markdown table | `markdown_table_generator` |
| [Acrewity AI Agent](workflows/acrewity-ai-agent/) | Natural language interface — say what you need, the AI picks the right service | All services |

| [HTML Invoice to PDF Email](workflows/html-invoice-to-pdf-email/) | Convert an HTML invoice to PDF and send it as an email attachment | `html_to_pdf` |
| [QR Codes for E-commerce](workflows/qr-codes-for-ecommerce/) | Batch-generate QR codes for a product catalog | `qr_code_generator` |
| [URL to Markdown LLM Pipeline](workflows/url-to-markdown-llm-pipeline/) | Fetch any URL as clean markdown, then summarize with Claude | `url_to_markdown` + Claude |
| [JSON Payload Validator](workflows/json-payload-validator/) | Validate webhook payloads against a JSON Schema; reject bad data with 422 | `json_schema_validator` |
| [Excel Upload to JSON](workflows/excel-upload-to-json/) | Receive an Excel file upload and convert each row to structured JSON | `excel_to_json` |

## About Acrewity

[Acrewity](https://acrewity.com) is an API platform with 20+ utility services for document generation, file conversion, QR codes, web scraping, email, and more. Install the community node once, access everything.

```
npm install n8n-nodes-acrewity
```

Or install via **Settings > Community Nodes** in n8n using the package name `n8n-nodes-acrewity`.

Free plan includes 100 credits/month. Each API call costs 1 credit.

## Contributing

Found a bug or want to improve a workflow? Open an issue or submit a pull request.
