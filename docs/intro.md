---
id: getting-started
slug: /
title: Getting Started
description: Turn any fillable PDF into a REST API with AI-powered field mapping. This guide covers upload, endpoints, authentication, examples, limits, errors, and best practices.
---

import Tabs from '@theme/Tabs'
import TabItem from '@theme/TabItem'

Welcome to DocuAPI. This guide shows how to upload a fillable PDF and generate a REST endpoint that accepts human‑readable JSON and returns a filled PDF.

## Prerequisites

- DocuAPI account
- An API key (Dashboard → API Keys)
- A fillable PDF
  - Recommended: AcroForm PDFs
  - XFA forms are not fully supported by most PDF libraries. If your PDF is XFA, export/print-to-PDF as a standard AcroForm in Acrobat (File → Save As Other → Reader Extended PDF or Print to PDF) or recreate fields as AcroForm.

## How it works

1. Upload a fillable PDF in the dashboard.
2. DocuAPI detects fields and generates AI‑powered, human‑readable aliases (e.g., `firstName`).
3. You receive two ways to call the API:
   - Submit endpoint (preferred): `/api/submit/<formId>`
   - Named path endpoint: `/api/forms/<saved-path>` (e.g., `/api/forms/1712345678901-abc123xyz`)
4. Send JSON to the endpoint; the response is a filled PDF (`application/pdf`).

## Quick Start

After upload, copy the submit endpoint: `/api/submit/<formId>` and call it with your API key.

<Tabs>
  <TabItem value="curl" label="cURL">

```bash
curl -X POST "https://your-domain.com/api/submit/<formId>" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: pk_your_api_key" \
  -d '{
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@example.com"
  }' --output filled-form.pdf
```

  </TabItem>
  <TabItem value="js" label="JavaScript">

```js
const res = await fetch('https://your-domain.com/api/submit/<formId>', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'X-API-Key': 'pk_your_api_key'
  },
  body: JSON.stringify({
    firstName: 'John',
    lastName: 'Doe',
    email: 'john@example.com'
  })
})
const blob = await res.blob()
const url = URL.createObjectURL(blob)
window.open(url)
```

  </TabItem>
  <TabItem value="python" label="Python">

```python
import requests

url = 'https://your-domain.com/api/submit/<formId>'
headers = {
  'Content-Type': 'application/json',
  'X-API-Key': 'pk_your_api_key'
}
payload = {
  'firstName': 'John',
  'lastName': 'Doe',
  'email': 'john@example.com'
}
r = requests.post(url, headers=headers, json=payload)
open('filled-form.pdf', 'wb').write(r.content)
```

  </TabItem>
</Tabs>

## AI Field Mapping

When you upload a PDF, DocuAPI detects and maps all fields. It also generates human‑readable names (e.g., `firstName`) so your JSON is simple and stable. Under the hood, we use Gemini 2.5 Flash‑Lite to inspect the PDF and infer better aliases from nearby labels.

Notes:
- You can still send the original PDF field names if you prefer (the API maps aliases and originals).
- Better results with clean AcroForm PDFs; XFA forms may carry verbose names (e.g., `topmostSubform[0].Page1[0].f1_01[0]`).

## HTTP Reference

### Submit endpoint (preferred)

- Method: `POST`
- Path: `/api/submit/<formId>`
- Headers: `Content-Type: application/json`, `X-API-Key: <key>`
- Body: JSON with field names → values (aliases or originals)
- Response: `application/pdf` (filled PDF)

### Named path endpoint

- Method: `POST`
- Path: `/api/forms/<saved-path>` (shown on the form’s API tab, e.g., `/api/forms/1712345678901-abc123xyz`)
- Headers/Body/Response: same as submit endpoint

### Inspect form fields (read-only)

- Method: `GET`
- Path: `/api/submit/<formId>`
- Response: form metadata including fields with `name`, `alias`, `type`, `required` and the active endpoint path.

## Error Handling

Responses follow this shape on error:

```json
{ "error": "string", "details": "optional" }
```

- 400 — validation failure / invalid JSON
- 401 — invalid API key
- 403 — unauthorized (endpoint not owned by key)
- 404 — form/endpoint not found or inactive
- 429 — rate limited
- 500 — server error

Tips:
- If you see `PDF does not contain fillable form fields`, your PDF may be flattened or XFA. Convert/export to AcroForm and re‑upload.
- If the response is HTML instead of JSON on error in browser console, log `await res.text()` to view details.

## Idempotency

Provide an `Idempotency-Key` header to de‑duplicate client retries. The service will echo the key back in the response headers.

## Rate Limits & Plans

- FREE: 50 API calls/month, 10MB storage, 5 forms
- Free Trial: 50 one‑time calls (consumed first)
- PRO: 1,500 API calls/month, 512MB storage, 10 forms

Notes:
- Usage is counted per user and resets monthly.
- Hitting limits returns 429 with usage details.

## Best Practices

- Validate inputs before calling the API; coerce types client‑side where possible.
- Cache generated PDFs on your side when appropriate to reduce repeat calls.
- Use aliases for readability; fall back to original names for exact compatibility.
- Keep API keys secret; call DocuAPI from your server or from protected environments.

## Next Steps

- Create an API key in Dashboard → API Keys
- Explore Fields to see mapped names, types, and whether they’re required
- Add webhooks to be notified of submissions
- Visit the Pricing page to upgrade if you need higher limits

## Troubleshooting

- "No fields detected" or many verbose names: your PDF is likely XFA. Export to AcroForm and re‑upload.
- 401/403 responses: verify `X-API-Key` and ownership of the endpoint.
- 405 on `/api/forms/...`: ensure you’re calling the exact saved path or use `/api/submit/<formId>`.