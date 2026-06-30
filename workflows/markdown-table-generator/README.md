# Markdown Table Generator (Demo)

Converts a JSON array into a formatted Markdown table using Acrewity. A simple building block for generating documentation, reports, email content, or any output that needs tabular data in Markdown format.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Manual Trigger** — Run manually to test
2. **Product Data** — A Set node with a sample JSON array of product records
3. **Generate Table** — Sends the JSON to Acrewity's `markdown_table_generator` and returns a Markdown table string

Replace the data in the Set node with any JSON array. The column headers are derived from the object keys.
