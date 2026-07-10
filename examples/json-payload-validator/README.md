# JSON Payload Validator

Validate incoming webhook payloads against a JSON Schema before processing them — reject bad data with a 422 before it pollutes your database or triggers downstream errors.

## What it does

1. Receives a POST request with a `data` object and a `schema` object
2. Validates `data` against `schema` using Acrewity's JSON Schema validator
3. If valid: routes to your processing logic and returns 200
4. If invalid: returns 422 with the specific validation errors

## Prerequisites

- **Acrewity community node** installed in n8n: `@acrewity/n8n-nodes-acrewity`
- **Acrewity account** with API key ([sign up free at acrewity.com](https://acrewity.com))

## Setup

1. Import `workflow.json` into n8n
2. Add your **Acrewity API** credential to the "Validate JSON Schema" node
3. Replace the "Process Valid Data" node with your actual business logic
4. Activate the workflow

## Test it — valid payload

```bash
curl -X POST https://your-n8n.com/webhook/validate-payload \
  -H "Content-Type: application/json" \
  -d '{
    "data": { "name": "Alice", "age": 30, "email": "alice@example.com" },
    "schema": {
      "type": "object",
      "required": ["name", "age", "email"],
      "properties": {
        "name": { "type": "string" },
        "age": { "type": "integer", "minimum": 0 },
        "email": { "type": "string", "format": "email" }
      }
    }
  }'
```

## Test it — invalid payload (missing required field)

```bash
curl -X POST https://your-n8n.com/webhook/validate-payload \
  -H "Content-Type: application/json" \
  -d '{
    "data": { "name": "Bob" },
    "schema": {
      "type": "object",
      "required": ["name", "age", "email"],
      "properties": {
        "name": { "type": "string" },
        "age": { "type": "integer" },
        "email": { "type": "string" }
      }
    }
  }'
```

Returns: `{ "success": false, "errors": ["..."] }` with HTTP 422.

## Advanced: hardcode your schema

Instead of passing the schema in the request body, hardcode it in the "Validate JSON Schema" node's `schema` parameter. Then callers only need to send their data — the schema is locked to your workflow.

## Credits used

**1 Acrewity credit per validation.**

## Related templates

- [Excel Upload to JSON](../excel-upload-to-json/) — parse and validate Excel uploads
