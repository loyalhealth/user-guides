---
name: Handling Responses
---

## Handling Responses

The API relies on HTTP status codes to communicate the status of your request.

- **200 OK** - Indicates that the request has succeeded.
- **204 No content** - The server has fulfilled the request but does not need to return a response body. The server may return the updated meta information.
- **400 Bad Request** - The request could not be understood by the server due to incorrect syntax. The client SHOULD NOT repeat the request without modifications.
- **401 Unauthorized** - Indicates that the request requires user authentication information. The client MAY repeat the request with a suitable Authorization header field.
- **403 Forbidden** - Unauthorized request. The client does not have access rights to the content. Unlike 401, the client’s identity is known to the server.
- **422 Unprocessable Entity** - The server understands the content type and syntax of the request entity, but still server is unable to process the request for some reason.
- **500 Internal Server Error** - The server encountered an unexpected condition that prevented it from fulfilling the request.
- **530 Internal Server Error** - An error on our side. Error description will be included in message.
