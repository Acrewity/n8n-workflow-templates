# PDF Document Generator (Invoice, Quote, Receipt, Estimate, Proforma)

Generates five types of professional PDF documents from a single webhook endpoint by switching on a `documentType` field. Eliminates the need for separate workflows or PDF libraries for each document type.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Webhook** — Listens for POST requests at `/generate-document`
2. **Build Document HTML** — Reads `documentType` from the payload and renders the appropriate HTML template with calculated subtotal, tax, and total
3. **Convert to PDF** — Sends HTML to Acrewity and receives a PDF
4. **Return PDF Response** — Returns `{ success, pdf (base64), filename, documentType }`

## Supported document types

| `documentType` | Title shown | Extra fields |
|---|---|---|
| `invoice` | INVOICE | Due date |
| `quote` | QUOTE | Valid until |
| `estimate` | ESTIMATE | Valid until |
| `receipt` | RECEIPT | Payment method |
| `proforma` | PROFORMA INVOICE | Due date |

## Sample request

```json
{
  "documentType": "quote",
  "company": "Your Company",
  "documentNumber": "QTE-2024-007",
  "customerName": "Jane Smith",
  "customerEmail": "jane@example.com",
  "validUntil": "2024-02-01",
  "taxRate": 0.13,
  "items": [
    { "name": "Website redesign", "quantity": 1, "price": 3500 }
  ]
}
```
