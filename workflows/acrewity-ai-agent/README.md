# Acrewity AI Agent

An AI agent that accepts natural language requests and autonomously calls the right Acrewity service to deliver the result — no code, no routing logic, just a message in and a file or result out.

**Example requests:**
- *"Generate a QR code for https://mysite.com"*
- *"Create a PDF invoice for Acme Corp, 3 items, $1,200 total"*
- *"Fetch the content of this blog post and summarize it: [URL]"*
- *"Show me what changed between these two contract drafts"*
- *"Convert this JSON data to an Excel file"*
- *"I need 5 random UUIDs"*

## How it works

```
POST /webhook/acrewity-agent
  { "message": "Generate a QR code for https://acrewity.com" }
  
→ AI Agent (Claude) receives the message
→ Selects the right tool from 6 available Acrewity services
→ Calls the Acrewity API with appropriate parameters
→ Returns the result

{ "success": true, "response": "QR code generated successfully. Here is the base64 PNG data: ..." }
```

## Tools available

| Tool | What it does |
|------|-------------|
| `generate_qr_code` | Encode any text or URL into a scannable QR image (PNG or SVG) |
| `convert_html_to_pdf` | Render HTML into a downloadable PDF — Claude writes styled HTML first |
| `fetch_url_as_markdown` | Fetch any webpage and return its content as clean Markdown |
| `generate_uuid` | Generate v1 or v4 UUIDs in any quantity |
| `compare_texts` | Compute a line-by-line diff between two text versions |
| `json_to_excel` | Convert a JSON array into a downloadable Excel spreadsheet |

## Setup

### Prerequisites
- n8n with the `@n8n/n8n-nodes-langchain` package (included in cloud and recent self-hosted)
- An [Acrewity API key](https://www.acrewity.com) (free tier available)
- An Anthropic API key (or swap the model node for OpenAI, Mistral, etc.)

### 1. Import the workflow

In n8n: **Workflows → Import from file** → upload `workflow.json`.

### 2. Configure your Acrewity API key

Each tool node sends requests to `https://www.acrewity.com/api/services/execute` with an `Authorization: Bearer YOUR_ACREWITY_API_KEY` header.

Replace `YOUR_ACREWITY_API_KEY` in each of the 6 tool nodes, or create a single n8n credential and reference it.

> Get your API key at [acrewity.com](https://www.acrewity.com) — free tier includes 100 requests/month.

### 3. Configure your AI model

The workflow uses Claude by default. Replace the `Claude (your model)` node with any supported model:
- **OpenAI**: swap for `@n8n/n8n-nodes-langchain.lmChatOpenAi`
- **Mistral**: swap for `@n8n/n8n-nodes-langchain.lmChatMistralCloud`
- **Ollama**: swap for `@n8n/n8n-nodes-langchain.lmChatOllama` (local)

### 4. Activate and test

Activate the workflow, then send a test request:

```bash
curl -X POST https://YOUR-N8N-URL/webhook/acrewity-agent \
  -H "Content-Type: application/json" \
  -d '{"message": "Generate 3 random UUIDs"}'
```

## API reference

**Endpoint:** `POST /webhook/acrewity-agent`

**Request:**
```json
{ "message": "Your natural language request here" }
```

**Response:**
```json
{
  "success": true,
  "response": "Agent's text response including any file data"
}
```

## Extending the agent

To add more Acrewity services, duplicate any existing tool node (type: **Code tool**) and update:
1. `name` — snake_case tool identifier (e.g. `convert_image_format`)
2. `description` — what it does and when to use it (the AI reads this)
3. `jsCode` — declare `$fromAI()` calls at the top of the code for each parameter the AI fills in, then call the Acrewity API via `fetch`

Example skeleton:
```javascript
const myParam = $fromAI('my_param', 'Description of the parameter');

const response = await fetch('https://www.acrewity.com/api/services/execute', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_ACREWITY_API_KEY'
  },
  body: JSON.stringify({
    service: 'your_service_id',
    operation: 'your_operation',
    parameters: { my_param: myParam }
  })
});

const data = await response.json();
return JSON.stringify(data);
```

All available Acrewity services: `uuid_generator`, `regex_matcher`, `text_diff`, `url_encoder_decoder`, `timezone_converter`, `json_schema_validator`, `url_to_markdown`, `html_to_pdf`, `html_to_markdown`, `markdown_to_html`, `qr_code_generator`, `markdown_table_generator`, `image_converter`, `excel_to_json`, `excel_editor`, `pdf_merge`, `pdf_extract_page`, `pdf_to_html`, `pdf_to_markdown`, `email_access`.

See the [Acrewity API docs](https://www.acrewity.com) for parameters.

## Related templates

- [Invoice PDF Generator](../invoice-pdf-generator/) — structured webhook → styled HTML → PDF
- [Web Page Summarizer](../web-page-summarizer/) — URL → Markdown → AI summary
- [SEO Page Analyzer](../seo-page-analyzer/) — URL → structured SEO report
