# Excel Upload to JSON

Receive an Excel (.xlsx) file upload, convert it to structured JSON, and process the rows — no Python scripts, no external services, just n8n and Acrewity.

## What it does

1. Receives a multipart form POST with an Excel file
2. Passes the file to Acrewity to convert to JSON
3. Returns each row as a structured JSON object

## Prerequisites

- **Acrewity community node** installed in n8n: `@acrewity/n8n-nodes-acrewity`
- **Acrewity account** with API key ([sign up free at acrewity.com](https://acrewity.com))

## Setup

1. Import `workflow.json` into n8n
2. Add your **Acrewity API** credential to the "Convert Excel to JSON" node
3. Optionally set the `sheet` parameter to read a specific sheet (default: `Sheet1`)
4. Add your processing logic inside the "Process Rows" Code node
5. Activate the workflow

## Test it

```bash
curl -X POST https://your-n8n.com/webhook/excel-to-json \
  -F "data=@/path/to/your/file.xlsx"
```

## Example response

Given an Excel file with columns `name`, `email`, `plan`:

```json
{
  "success": true,
  "total_rows": 3,
  "rows": [
    { "name": "Alice", "email": "alice@example.com", "plan": "Pro" },
    { "name": "Bob", "email": "bob@example.com", "plan": "Starter" },
    { "name": "Carol", "email": "carol@example.com", "plan": "Business" }
  ]
}
```

## Common use cases

- **Bulk import:** Upload a customer list from Excel into a CRM or database
- **Report processing:** Receive weekly Excel reports and push data to Supabase/Airtable
- **Data migration:** Convert legacy spreadsheets to API-ready JSON
- **Validation pipeline:** Combine with the [JSON Payload Validator](../json-payload-validator/) template to check Excel data before importing

## Credits used

**1 Acrewity credit per Excel file** (regardless of row count).

## Related templates

- [JSON Payload Validator](../json-payload-validator/) — validate data before processing
- [HTML Invoice to PDF Email](../html-invoice-to-pdf-email/) — generate PDFs from processed data
