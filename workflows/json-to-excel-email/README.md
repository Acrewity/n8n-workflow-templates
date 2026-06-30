# JSON to Excel & Email

Accepts a JSON array via webhook, converts it to a formatted Excel file using Acrewity, and emails it to a specified address. Eliminates the need for server-side Excel libraries when building automated reporting workflows.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com)) — used for both Excel generation and email sending
- n8n with the `n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**
4. In the **Send Email** node, update the SMTP parameters with your email server details

## How it works

1. **Webhook** — Listens for POST requests at `/json-to-excel`
2. **Convert to Excel** — Sends the JSON data array to Acrewity's `json_to_excel` service
3. **Set Email Data** — Prepares the recipient address, subject, and body
4. **Send Email** — Delivers the report notification via Acrewity's email service
5. **Respond** — Returns success confirmation

## Sample request

```json
{
  "email": "reports@yourcompany.com",
  "subject": "Monthly Sales Report",
  "sheet_name": "Sales",
  "data": [
    { "month": "January", "revenue": 12000, "expenses": 8000 },
    { "month": "February", "revenue": 15000, "expenses": 9500 }
  ]
}
```

## Note on email

This workflow uses Acrewity's built-in email service. Update the SMTP fields in the Send Email node with your own SMTP host, username, password, and from address.
