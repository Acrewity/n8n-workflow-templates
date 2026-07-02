# HTML Invoice to PDF Email

Convert an HTML invoice template to a PDF and send it as an email attachment — all inside n8n using the Acrewity community node.

## What it does

1. Receives a POST request with HTML content, recipient email, and subject
2. Converts the HTML to a PDF using Acrewity
3. Prepares the PDF as an email attachment
4. Sends the email with the PDF attached via SMTP
5. Returns a success response

## Prerequisites

- **Acrewity community node** installed in n8n: `@acrewity/n8n-nodes-acrewity`
- **Acrewity account** with API key ([sign up free at acrewity.com](https://acrewity.com))
- **SMTP credentials** configured in n8n (Gmail, SendGrid, or any SMTP provider)

## Setup

1. Import `workflow.json` into n8n (Workflows → Import from file)
2. Add your **Acrewity API** credential to the "Convert HTML to PDF" node
3. Add your **SMTP** credential to the "Send Invoice Email" node
4. Activate the workflow
5. Send a test request (see below)

## Test it

```bash
curl -X POST https://your-n8n.com/webhook/generate-invoice-pdf \
  -H "Content-Type: application/json" \
  -d '{
    "to": "customer@example.com",
    "subject": "Invoice #1001",
    "message": "Please find your invoice attached.",
    "html": "<html><body><h1>Invoice #1001</h1><p>Amount due: $150.00</p><p>Due date: 2026-08-01</p></body></html>"
  }'
```

## Example HTML invoice

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body { font-family: Arial, sans-serif; padding: 40px; color: #333; }
    h1 { color: #2c3e50; border-bottom: 2px solid #eee; padding-bottom: 10px; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; }
    th { background: #2c3e50; color: white; padding: 10px; text-align: left; }
    td { padding: 10px; border-bottom: 1px solid #eee; }
    .total { font-weight: bold; font-size: 1.2em; }
  </style>
</head>
<body>
  <h1>Invoice #1001</h1>
  <p><strong>To:</strong> Acme Corp</p>
  <p><strong>Date:</strong> 2026-07-01</p>
  <p><strong>Due:</strong> 2026-08-01</p>
  <table>
    <tr><th>Item</th><th>Qty</th><th>Price</th><th>Total</th></tr>
    <tr><td>Consulting (hrs)</td><td>10</td><td>$100</td><td>$1,000</td></tr>
    <tr><td>Setup fee</td><td>1</td><td>$250</td><td>$250</td></tr>
    <tr><td colspan="3" class="total">Total Due</td><td class="total">$1,250</td></tr>
  </table>
</body>
</html>
```

## Credits used

Each workflow run uses **1 Acrewity credit** (for the HTML→PDF conversion).

## Related templates

- [Acrewity AI Agent](../acrewity-ai-agent/) — AI assistant with 25 built-in Acrewity tools
