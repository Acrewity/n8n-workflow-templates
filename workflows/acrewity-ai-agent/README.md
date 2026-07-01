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

This template uses **two workflows** — import and activate both:

```
POST /webhook/acrewity-agent
  { "message": "Generate a QR code for https://acrewity.com" }

→ Main Agent workflow receives the message
→ AI selects the right tool from 14 Acrewity services
→ Tool calls the Dispatcher workflow (sub-workflow)
→ Dispatcher builds the request body and calls Acrewity API
→ Result returns up through the chain

{ "success": true, "response": "QR code generated. Base64 PNG: ..." }
```

**Why two workflows?** n8n's AI tool nodes (`toolWorkflow`) call sub-workflows to make HTTP requests. This is the only approach that reliably passes `$fromAI()` parameters through to Anthropic's tool schema while allowing real HTTP calls.

## Tools available

| Tool | What it does |
|------|-------------|
| `generate_qr_code` | Encode any text or URL into a scannable QR image (PNG or SVG) |
| `convert_html_to_pdf` | Render HTML into a downloadable PDF — Claude writes styled HTML first |
| `fetch_url_as_markdown` | Fetch any webpage and return its content as clean Markdown |
| `generate_uuid` | Generate random UUIDs in any quantity |
| `compare_texts` | Compute a line-by-line diff between two text versions |
| `json_to_excel` | Convert a JSON array into a downloadable Excel spreadsheet |
| `convert_html_to_markdown` | Convert HTML content into clean Markdown text |
| `convert_image` | Convert an image between JPEG, PNG, and WebP formats (requires public URL) |
| `validate_json_schema` | Validate a JSON object against a JSON Schema, returns errors if any |
| `generate_markdown_table` | Generate a formatted Markdown table from headers and row data |
| `convert_markdown_to_html` | Convert Markdown into a full HTML document with optional styling |
| `match_regex` | Run a regex pattern against text and return all matches |
| `convert_timezone` | Convert a datetime between timezone abbreviations (UTC, EST, PST, CET, JST…) |
| `encode_or_decode_url` | URL-encode or URL-decode any string |

## Setup

### Prerequisites
- n8n (self-hosted or cloud) with the `@n8n/n8n-nodes-langchain` package
- An [Acrewity API key](https://www.acrewity.com) (free tier available)
- An Anthropic API key (or swap the model node for OpenAI, Mistral, etc.)

### Step 1 — Import and configure the Dispatcher

1. In n8n: **Workflows → Import from file** → upload `dispatcher.json`
2. Open the imported **Acrewity API Dispatcher** workflow
3. Click the **Call Acrewity API** node
4. Replace `YOUR_ACREWITY_API_KEY` in the Authorization header with your actual key
5. **Save** the workflow
6. **Activate** the workflow (toggle in the top-right) — this step is required
7. Copy the workflow **ID** from the URL bar (e.g. `https://your-n8n.com/workflow/abc123xyz` → ID is `abc123xyz`)

> **Important:** The dispatcher must be active before the main agent will work. n8n cannot call inactive sub-workflows.

### Step 2 — Import and configure the Main Agent

1. In n8n: **Workflows → Import from file** → upload `workflow.json`
2. Open the imported **Acrewity AI Agent** workflow
3. For each of the 6 tool nodes (`generate_qr_code`, `convert_html_to_pdf`, etc.):
   - Click the node
   - In the **Workflow** field, replace `YOUR_DISPATCHER_WORKFLOW_ID` with the ID you copied in Step 1
4. Click the **Claude (your model)** node and select your Anthropic credential
5. **Save** the workflow
6. **Activate** the workflow

### Step 3 — Test

```bash
curl -X POST https://YOUR-N8N-URL/webhook/acrewity-agent \
  -H "Content-Type: application/json" \
  -d '{"message": "Generate 3 random UUIDs"}'
```

Expected response:
```json
{
  "success": true,
  "response": "Here are 3 UUIDs: ..."
}
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
  "response": "Agent's text response including any file data or results"
}
```

## Changing the AI model

The workflow uses Claude by default. To use a different model, replace the **Claude (your model)** node:

| Model | n8n node type |
|-------|--------------|
| OpenAI GPT | `@n8n/n8n-nodes-langchain.lmChatOpenAi` |
| Mistral | `@n8n/n8n-nodes-langchain.lmChatMistralCloud` |
| Google Gemini | `@n8n/n8n-nodes-langchain.lmChatGoogleGemini` |
| Ollama (local) | `@n8n/n8n-nodes-langchain.lmChatOllama` |

## Extending the agent

To add more Acrewity services:

1. Duplicate any existing tool node (type: **Workflow tool**)
2. Update the node's `name` and `description`
3. In **Workflow Inputs**, set `service` and `operation` to the Acrewity API values, and add `$fromAI()` expressions for any parameters the AI should fill in
4. Connect the new node to the AI Agent node via the `ai_tool` output

The dispatcher automatically handles any new service/operation combinations — no changes needed there (except for `json-to-excel`, which has special parameter handling already built in).

**Available Acrewity service IDs:** `uuid_generator`, `regex_matcher`, `text-diff`, `url_encoder_decoder`, `timezone_converter`, `json_schema_validator`, `url_to_markdown`, `html_to_pdf`, `html_to_markdown`, `markdown_to_html`, `qr_code_generator`, `markdown_table_generator`, `image_converter`, `excel_to_json`, `json-to-excel`, `pdf_merge`, `pdf_extract_page`, `pdf_to_html`, `pdf_to_markdown`, `email_access`.

See the [Acrewity API docs](https://www.acrewity.com/docs) for each service's parameters.

## Troubleshooting

**Agent responds without calling any tools**
- Check that the Dispatcher workflow is active (Step 1, point 6 above)
- Verify the dispatcher workflow ID is correctly set in all 6 tool nodes

**"Workflow is not active" error**
- Go to the Dispatcher workflow and activate it

**Tool returns an error from Acrewity**
- Verify your API key is correct in the Dispatcher's HTTP Request node
- Check your Acrewity credit balance at [acrewity.com](https://www.acrewity.com)

## Related templates

- [Invoice PDF Generator](../invoice-pdf-generator/) — structured webhook → styled HTML → PDF
- [Web Page Summarizer](../web-page-ai-summarizer/) — URL → Markdown → AI summary
- [SEO Page Analyzer](../seo-page-analyzer/) — URL → structured SEO report
