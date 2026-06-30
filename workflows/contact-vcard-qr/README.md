# Contact vCard QR Generator

Accepts contact details via webhook and returns a QR code encoding a vCard 3.0 record. When scanned, the QR code adds the contact directly to the user's phone — useful for business cards, event badges, and conference networking apps.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com))
- n8n with the `n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**

## How it works

1. **Webhook** — Listens for POST requests at `/contact-qr`
2. **Build vCard** — Constructs a vCard 3.0 string from the contact fields
3. **Generate QR Code** — Encodes the vCard into a 400px PNG QR code via Acrewity
4. **Return QR Code** — Returns `{ success, contact, qrCode (base64) }`

## Sample request

```json
{
  "firstName": "Jane",
  "lastName": "Smith",
  "company": "Acme Corp",
  "title": "Product Manager",
  "phone": "+1-555-867-5309",
  "email": "jane@acme.com",
  "website": "https://acme.com"
}
```
