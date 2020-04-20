---
name: Handling Responses
---

# Handling Responses

The API relies on HTTP status codes to communicate the status of your request.

- **200 — Success**
  - Everything went smooth.
- **204 — No content**
  - We could get your request, but there was no content to return
- **400 — Bad Request**
  - Malformed JSON payload.
- **401 — Authentication URL Params (Required)**
  - Missing or invalid API token.
- **403 — Forbidden**
  - Attempting to perform a restricted action.
- **422 — Unprocessable Entity**
  - Something is not right with the request data.
- **500 — Internal Server Error**
  - An error on our side. Please contact support if the error persists.
- **530 — Internal Server Error**
  - An error on our side. Error description will be included in message
