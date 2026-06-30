# URL Content Diff

Fetches two web pages, extracts their text content, and returns a structured diff showing what changed between them. Useful for monitoring competitor pages, tracking documentation changes, or auditing content updates.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Webhook** — Listens for POST requests with two URLs
2. **Fetch URL 1** — Converts the first URL to Markdown via Acrewity
3. **Fetch URL 2** — Converts the second URL to Markdown via Acrewity
4. **Prepare Texts** — Extracts the text content from both results
5. **Compare Content** — Sends both texts to Acrewity's `text_diff` service
6. **Respond** — Returns the diff result

## Sample request

```json
{
  "url1": "https://example.com/page-v1",
  "url2": "https://example.com/page-v2"
}
```
