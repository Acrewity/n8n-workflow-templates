# QR Codes for E-commerce Products

Batch-generate QR codes for an entire product catalog — one webhook call, one QR per product, all returned in a single JSON response.

## What it does

1. Receives a POST request with an array of products (each with a `url` or `sku` and `name`)
2. Loops through each product and generates a QR code using Acrewity
3. Collects all results and returns them as a JSON array

## Prerequisites

- **Acrewity community node** installed in n8n: `@acrewity/n8n-nodes-acrewity`
- **Acrewity account** with API key ([sign up free at acrewity.com](https://acrewity.com))

## Setup

1. Import `workflow.json` into n8n
2. Add your **Acrewity API** credential to the "Generate QR Code" node
3. Activate the workflow

## Test it

```bash
curl -X POST https://your-n8n.com/webhook/generate-product-qr-codes \
  -H "Content-Type: application/json" \
  -d '[
    { "sku": "PROD-001", "name": "Blue T-Shirt", "url": "https://shop.example.com/products/PROD-001" },
    { "sku": "PROD-002", "name": "Red Hat", "url": "https://shop.example.com/products/PROD-002" },
    { "sku": "PROD-003", "name": "Green Mug", "url": "https://shop.example.com/products/PROD-003" }
  ]'
```

## Example response

```json
{
  "success": true,
  "count": 3,
  "products": [
    { "sku": "PROD-001", "name": "Blue T-Shirt", "qr_base64": "iVBOR...", "qr_url": "https://shop.example.com/products/PROD-001" },
    { "sku": "PROD-002", "name": "Red Hat", "qr_base64": "iVBOR...", "qr_url": "https://shop.example.com/products/PROD-002" },
    { "sku": "PROD-003", "name": "Green Mug", "qr_base64": "iVBOR...", "qr_url": "https://shop.example.com/products/PROD-003" }
  ]
}
```

The `qr_base64` field is a base64-encoded PNG you can embed directly in an `<img src="data:image/png;base64,..."` tag or save to disk.

## Credits used

**1 Acrewity credit per product.** 100 products = 100 credits.

## Use cases

- Print QR stickers for product packaging
- Generate QR codes for a catalog PDF
- Display QR codes on product detail pages
- Link physical products to landing pages

## Related templates

- [HTML Invoice to PDF Email](../html-invoice-to-pdf-email/) — generate and email PDF invoices
