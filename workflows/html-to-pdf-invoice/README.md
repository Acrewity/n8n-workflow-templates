# HTML to PDF Invoice (Demo)

A minimal demo showing how to convert any HTML string into a PDF using Acrewity. Useful as a starting point for building custom document generation workflows.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `@acrewity/n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `@acrewity/n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Manual Trigger** — Run manually to test
2. **Set Invoice HTML** — Provides a sample HTML invoice string
3. **Generate PDF** — Sends HTML to Acrewity's `html_to_pdf` service and returns the PDF

Replace the HTML in the Set node with your own template to generate any PDF document.
