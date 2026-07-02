# URL to Markdown for LLM Pipelines

Turn any URL into clean markdown — then feed it directly into an AI node. No scraping code, no HTML parsing, no boilerplate.

## What it does

1. Receives a POST request with a URL
2. Fetches the page and converts it to clean markdown using Acrewity
3. Passes the markdown to Claude for summarization
4. Returns both the full markdown and the AI summary

## Prerequisites

- **Acrewity community node** installed in n8n: `@acrewity/n8n-nodes-acrewity`
- **Acrewity account** with API key ([sign up free at acrewity.com](https://acrewity.com))
- **Anthropic API key** for the Claude node (or swap for any other LLM)

## Setup

1. Import `workflow.json` into n8n
2. Add your **Acrewity API** credential to the "Fetch URL as Markdown" node
3. Add your **Anthropic** credential to the "Claude" node
4. Activate the workflow

## Test it

```bash
curl -X POST https://your-n8n.com/webhook/url-to-markdown \
  -H "Content-Type: application/json" \
  -d '{ "url": "https://en.wikipedia.org/wiki/Automation" }'
```

## Adapt for your use case

- **Research assistant:** Replace the summarization prompt with "extract key facts" or "find all statistics"
- **Competitive monitoring:** Schedule a trigger instead of a webhook, feed in competitor URLs
- **Content pipeline:** Strip the AI node entirely and use the markdown field directly as input to a writing tool
- **RAG pipeline:** Chunk the `markdown` field and upsert into a vector store (Supabase, Pinecone, etc.)

## Credits used

**1 Acrewity credit per URL.** The Claude call is billed to your Anthropic account separately.

## Related templates

- [HTML Invoice to PDF Email](../html-invoice-to-pdf-email/) — generate PDFs from HTML
