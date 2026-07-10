# QR Code Generator (Demo)

Generates a QR code image from any text or URL using Acrewity. A starting point for embedding QR generation into any n8n workflow — product labels, links, confirmations, or event tickets.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `@acrewity/n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `@acrewity/n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Manual Trigger** — Run manually to test
2. **Set QR Data** — Sets the URL or text to encode, and the output size in pixels
3. **Generate QR Code** — Calls Acrewity's `qr_code_generator` service and returns a PNG/SVG image

Change the `text` value in the Set node to encode any URL, contact info, or plain text.
