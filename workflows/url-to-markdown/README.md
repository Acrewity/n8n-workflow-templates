# URL to Markdown Converter (Demo)

Fetches a web page and converts its content to clean Markdown using Acrewity. Useful as a building block for content pipelines, AI summarizers, documentation scrapers, and change monitors.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Manual Trigger** — Run manually to test
2. **Set URL** — Sets the target URL (default: `https://example.com`)
3. **Convert to Markdown** — Fetches the page and converts HTML to Markdown via Acrewity's `url_to_markdown` service

Change the URL in the Set node to point to any public web page.
