# SEO Page Analyzer

Fetches a web page, extracts its content, and runs it through an AI model to produce a structured SEO report. Returns keyword analysis, heading structure, readability score, SEO score, issues, and recommendations — all as JSON.

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
2. **Fetch Page Content** — Converts the page to Markdown via Acrewity's `url_to_markdown`
3. **SEO Analyst** — An AI agent (Claude) analyzes the content and returns structured JSON
4. **Respond** — Returns the full SEO report

## Sample request

```json
{ "url": "https://yoursite.com/landing-page" }
```

## Sample response fields

```json
{
  "title": "Page title",
  "word_count": 842,
  "h1_tags": ["Main heading"],
  "h2_tags": ["Section 1", "Section 2"],
  "top_keywords": [{ "word": "automation", "count": 12 }],
  "readability_score": 7,
  "seo_score": 74,
  "issues": ["Missing meta description", "Only one H1"],
  "recommendations": ["Add alt text to images", "Increase internal linking"]
}
```
