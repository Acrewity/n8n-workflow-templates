# Generate and email invoices, quotes, and receipts from webhook JSON

Connect any system that knows about orders — an online store, CRM, booking tool, or internal app — and every POST becomes a professional PDF delivered to the customer's inbox.

## Who's it for

Anyone whose system already has order data but no billing-document infrastructure. Instead of returning a raw file for you to handle, this workflow completes the job: the customer gets the document, your system gets a confirmation.

## How it works

1. Your system POSTs order JSON to the webhook — `documentType` picks invoice, quote, estimate, receipt, or proforma
2. The workflow builds a styled document with line items, tax, and totals
3. The Acrewity community node renders it to PDF
4. Gmail delivers the PDF to the customer within seconds
5. The caller receives a JSON confirmation with the document number
6. Bad payloads (missing email, broken or missing items) receive a clear HTTP 400 with the reason — never a silent failure

## Requirements

- n8n with the verified community node `@acrewity/n8n-nodes-acrewity` installed
- Acrewity API key — free at [acrewity.com](https://acrewity.com) (100 free credits/month, 1 credit per PDF)
- Gmail credential connected in n8n

## How to set up

1. Import `workflow.json` (Workflows > Import from file)
2. Add your Acrewity API credential to "Convert document to PDF" and your Gmail credential to "Email document to customer"
3. Edit "Workflow configuration": company name, logo URL, default tax rate, currency
4. Activate, then POST to the webhook URL:

```json
{
  "documentType": "invoice",
  "documentNumber": "INV-2026-001",
  "customerName": "John Smith",
  "customerEmail": "john@example.com",
  "dueDate": "2026-08-15",
  "taxRate": 0.13,
  "items": [{"name": "Widget", "quantity": 2, "price": 9.99}]
}
```

## How to customize

The document layout lives in "Build document HTML" (the editable spots are marked CHANGE ME), the email copy in the Gmail node. Add a Google Drive node after Gmail to archive every document, or a Slack node to notify your team.
