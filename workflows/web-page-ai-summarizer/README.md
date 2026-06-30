# Web Page AI Summarizer

Fetches any web page, converts it to text, and runs it through an AI agent to produce a structured summary. Useful for news digests, competitive research, content monitoring, and research pipelines.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- Anthropic API key for the Claude AI model
- n8n with the `n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**
4. Add your Anthropic credential: **Credentials > New > Anthropic**

## How it works

1. **Webhook** — Listens for POST requests with a `url` field
2. **Extract Page Content** — Fetches the page and converts it to Markdown via Acrewity's `url_to_markdown` service
3. **AI Agent** — Passes the Markdown content to a Claude model with a summarization prompt
4. **Respond** — Returns the AI-generated summary

## Sample request

```json
{
  "url": "https://example.com/article"
}
```
