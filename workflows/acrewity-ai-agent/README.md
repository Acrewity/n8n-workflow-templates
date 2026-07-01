# Acrewity AI Agent for n8n

An AI Agent powered by Claude that gives it access to 25 Acrewity utility services — PDF processing, QR codes, data conversion, web scraping, and more — directly through the Acrewity community node.

## Prerequisites

- n8n 2.x with the **Acrewity community node** installed: `@acrewity/n8n-nodes-acrewity` v0.2.2+
- An **Acrewity API key** (get one at [acrewity.com](https://acrewity.com))
- An **Anthropic API key** for Claude

## Setup

1. **Install the community node** — n8n Settings → Community Nodes → Install → `@acrewity/n8n-nodes-acrewity`
2. **Import this workflow** — copy `workflow.json` and import via n8n → Workflows → Import
3. **Add credentials**:
   - Create an **Acrewity API** credential with your API key and assign it to all Acrewity nodes
   - Create an **Anthropic** credential with your API key and assign it to the Claude model node
4. **Activate** the workflow
5. **Test** by sending a POST request to the webhook URL with `{ "message": "Generate 3 UUIDs" }`

## Available tools (25)

| Tool | What it does |
|------|-------------|
| Generate UUID | Generate random v1 or v4 UUIDs |
| Generate QR Code | Create QR code images from text or URLs |
| Generate Barcode | Create 1D barcode images (Code128, EAN, UPC) |
| Match Regex | Run regex patterns against text |
| Compare Texts | Line-by-line diff between two texts |
| URL Encode | Percent-encode a string for URLs |
| URL Decode | Decode a percent-encoded string |
| Convert Timezone | Convert datetimes between timezones |
| Generate Markdown Table | Build a Markdown table from headers and rows |
| Validate JSON Schema | Validate JSON data against a JSON Schema |
| Fetch URL as Markdown | Fetch a webpage and convert to Markdown |
| HTML to PDF | Render HTML as a downloadable PDF |
| HTML to Markdown | Convert HTML to clean Markdown |
| Markdown to HTML | Convert Markdown to a styled HTML document |
| Markdown to HTML Fragment | Convert Markdown to an HTML fragment |
| Convert Image | Convert images between formats (JPEG, PNG, WebP) |
| JSON to Excel | Convert JSON array to a single-sheet Excel file |
| JSON to Multi-Sheet Excel | Create a multi-sheet Excel workbook from JSON |
| Extract Links | Extract all links from a webpage |
| Generate Sitemap | Generate an XML sitemap from URLs |
| PDF to Markdown | Convert PDF files to Markdown text |
| PDF to HTML | Convert PDF files to HTML |
| Merge PDFs | Merge multiple PDF files into one |
| Excel to JSON | Convert Excel files to JSON |
| Send Email | Send email via SMTP |

## Architecture

```
Webhook → AI Agent (Claude) → 25 Acrewity nodes (ai_tool)
```

Each Acrewity node is configured for a specific service and operation and connected directly to the AI Agent via the `ai_tool` port. No dispatcher sub-workflow needed.

## Usage

Send a POST request to the webhook URL:

```bash
curl -X POST https://your-n8n.com/webhook/acrewity-agent \
  -H "Content-Type: application/json" \
  -d '{"message": "Convert this HTML to a PDF: <h1>Hello World</h1>"}'
```

The agent will pick the right tool(s), call the Acrewity API, and return the result.
