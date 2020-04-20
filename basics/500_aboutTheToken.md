---
name: About the API Token
---

## About the API Token

Loyal API uses JSON Web Tokens (JWTs) to authenticating requests.

The scopes claim of this token indicates which actions can be performed with it when calling this API. For example, this token would grant read-only access to users and read/write access to rules. Trying to perform any other action will result in a 403 Forbidden response.
