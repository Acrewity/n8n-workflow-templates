# Acrewity AI Agent — n8n Workflow Template

A production-ready AI Agent workflow that connects Claude Sonnet to 18 Acrewity utility tools via the official `@acrewity/n8n-nodes-acrewity` community node.

## Architecture

```
POST /webhook/acrewity-agent
         │
         ▼
    Webhook node
         │
         ▼
    AI Agent (Claude Sonnet 4.6)
    ├── generate_uuid
    ├── generate_qr_code
    ├── generate_barcode
    ├── match_regex
    ├── compare_texts
    ├── encode_url
    ├── decode_url
    ├── convert_timezone
    ├── generate_markdown_table
    ├── validate_json_schema
    ├── fetch_url_as_markdown
    ├── convert_html_to_pdf
    ├── convert_html_to_markdown
    ├── convert_markdown_to_html
    ├── convert_image
    ├── json_to_excel
    ├── extract_links
    └── generate_sitemap
         │
         ▼
    Respond to Webhook
```

Each Acrewity node uses `$fromAI()` expressions so the AI agent fills in the parameters dynamically based on the user's request.

## Prerequisites

1. **n8n** with the `@acrewity/n8n-nodes-acrewity` community node installed
2. **Acrewity API key** — get one at [acrewity.com](https://acrewity.com)
3. **Anthropic API key** — for Claude Sonnet 4.6

## Setup

1. Install the community node in n8n:
   - Go to **Settings → Community Nodes → Install**
   - Enter: `@acrewity/n8n-nodes-acrewity`

2. Import `workflow.json` into n8n

3. Set up credentials:
   - **Acrewity account**: Add your API key
   - **Anthropic account**: Add your API key

4. Activate the workflow

5. Test with a POST request:
   ```bash
   curl -X POST https://your-n8n.example.com/webhook/acrewity-agent \
     -H "Content-Type: application/json" \
     -d '{"message": "Generate 5 UUIDs"}'
   ```

## Request Format

```json
{ "message": "your request here" }
```

## Response Format

```json
{ "success": true, "response": "agent reply here" }
```

## Tools Reference

| Tool | Resource | Operation | Key Parameters |
|------|----------|-----------|----------------|
| generate_uuid | uuid_generator | generate_uuid | version (v1/v4), count |
| generate_qr_code | qr_code_generator | generate_qr | text, format, size |
| generate_barcode | barcode_generator | generate_barcode | text |
| match_regex | regex_matcher | match_pattern | text, pattern, flags |
| compare_texts | text_diff | compare_text | text1, text2, format |
| encode_url | url_encoder_decoder | encode | text |
| decode_url | url_encoder_decoder | decode | text |
| convert_timezone | timezone_converter | convert_timezone | datetime, fromTimezone, toTimezone |
| generate_markdown_table | markdown_table_generator | generate_table | headers, rows |
| validate_json_schema | json_schema_validator | validate_json | data, schema |
| fetch_url_as_markdown | url_to_markdown | url_to_markdown | url |
| convert_html_to_pdf | html_to_pdf | convert_pdf | html |
| convert_html_to_markdown | html_to_markdown | convert | content, preserve_tables |
| convert_markdown_to_html | markdown_to_html | convert | content, include_styles, highlight_code |
| convert_image | image_converter | convert_image | imageUrl, format, quality |
| json_to_excel | json_to_excel | create_excel | data, sheetName |
| extract_links | sitemap_generator | extract_links | url |
| generate_sitemap | sitemap_generator | generate_sitemap | url |

## Community Node

Source: [github.com/Acrewity/acrewity-n8n](https://github.com/Acrewity/acrewity-n8n)  
Package: [`@acrewity/n8n-nodes-acrewity`](https://www.npmjs.com/package/@acrewity/n8n-nodes-acrewity)