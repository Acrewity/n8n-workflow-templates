# Invoice PDF Generator

Accepts order data via webhook and returns a styled PDF invoice. Solves the common problem of generating professional invoices programmatically without setting up a PDF rendering server.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `@acrewity/n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `@acrewity/n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Webhook** — Listens for POST requests at `/generate-invoice`
2. **Build Invoice HTML** — Constructs a styled HTML invoice from the request body (customer name, line items, tax rate, currency)
3. **Convert to PDF** — Sends the HTML to Acrewity's `html_to_pdf` service and receives a PDF
4. **Respond** — Returns the PDF as base64 JSON

## Sample request

```json
{
  "customer_name": "Acme Corp",
  "customer_email": "billing@acme.com",
  "invoice_number": "INV-2024-042",
  "date": "2024-01-15",
  "due_date": "2024-02-15",
  "currency": "USD",
  "tax_rate": 0.10,
  "items": [
    { "name": "Consulting", "qty": 5, "price": 150 },
    { "name": "Setup fee", "qty": 1, "price": 200 }
  ]
}
```
