---
id: getting-started
slug: /
title: Getting Started
description: Turn any fillable PDF into a REST API with AI-powered field mapping.
---

import Tabs from '@theme/Tabs'
import TabItem from '@theme/TabItem'

Welcome to DocuAPI. This guide shows how to upload a fillable PDF and generate a REST endpoint that accepts human‑readable JSON and returns a filled PDF.

## Prerequisites

- DocuAPI account
- An API key (create one in Dashboard → API Keys)
- A fillable PDF (AcroForm/XFA)

## Quick Start

1. Upload your PDF in the dashboard.
2. Copy the generated endpoint: `/api/submit/<form-id>`
3. Send JSON with AI‑generated field names.

<Tabs>
  <TabItem value="curl" label="cURL">

```bash
curl -X POST "https://your-domain.com/api/submit/<form-id>" \
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
const res = await fetch('https://your-domain.com/api/submit/<form-id>', {
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

url = 'https://your-domain.com/api/submit/<form-id>'
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

When you upload a PDF, DocuAPI detects and maps all fields. It also generates human‑readable names (e.g., `firstName`), so your JSON is simple and stable.

> You can still send the original PDF field names if you prefer.

## HTTP Reference

- Method: `POST`
- Path: `/api/submit/<form-id>`
- Headers: `Content-Type: application/json`, `X-API-Key: <key>`
- Body: JSON with field names → values
- Response: `application/pdf` (filled PDF)

## Error Handling

Responses follow this shape on error:

```json
{ "error": "string", "details": "optional" }
```

- 400 — validation failure
- 401 — invalid API key
- 404 — form inactive or not found
- 429 — rate limited
- 500 — server error

## Best Practices

- Validate inputs on your side before calling the API
- Store generated PDFs if you need to re‑download them later
- Keep API keys secret (server side)

## Next Steps

- Create an API key in Dashboard → API Keys
- Explore Fields to see mapped names and types
- Add webhooks to be notified of submissions