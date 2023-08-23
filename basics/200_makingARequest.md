---
name: 'Making a request'
---

## Making a Request

Calls to the Loyal API will need the `Authorization` HTTP header using the [Bearer authentication scheme](https://tools.ietf.org/html/draft-ietf-oauth-v2-bearer-20#section-2.1).

In order to get your token to pass in your `Authorization` header, you'll first need to make a general `POST` call to our `token` endpoint along with your [*API Key*](/basics/developer-guide#how-do-i-get-an-api-key).

### Getting a token

This endpoint returns a JSON object containing the token you can use to authenticate API requests.

`https://api.loyalhealth.com/auth/client/token`

Examples of making this API request:

```csharp
namespace ClientApiAuthorization
{
    class Program
    {
        private static readonly HttpClient HttpClient = new HttpClient();
        static async Task Main(string[] args)
        {
            var myApiKey = @"***my api key***";
            var tokenUrl = @"https://api.loyalhealth.com/auth/client/token";
            // request a token
            var tokenRequest = new HttpRequestMessage(HttpMethod.Post, tokenUrl);
            tokenRequest.Headers.Add("Authorization", $@"ApiKey {myApiKey}");
            var tokenResponse = await HttpClient.SendAsync(tokenRequest);
            var authorizationResponse = JsonConvert.DeserializeObject<AuthorizationResponse>(await tokenResponse.Content.ReadAsStringAsync());
        }
    }
    class AuthorizationResponse
    {
        public bool Authenticated { get; set; }
        public string Token {get; set; }
    }
}
```

```javascript
const request = require('request');
let token = null;

const options = {
  method: 'POST',
  url: 'https://api.loyalhealth.com/auth/client/token',
  headers: {
    Authorization: `ApiKey ${process.env.APIKEY}`
  }
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    token = body.token;
  }
}

request(options, callback); // make new calls using set token
```

Return example:

```http
HTTP/1.1 200 OK
{
    "authenticated": true,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy5taWNyb3NvZnQuY29tL3dzLzIwMDgvMDYvaWRlbnRpdHkvY2xhaW1zL3JvbGUiOiJMb3lhbEFwaUNsaWVudEFjY2VzcyIsImh0dHA6Ly9zY2hlbWFzLnhtbHNvYXAub3JnL3dzLzIwMDUvMDUvaWRlbnRpdHkvY2xhaW1zL25hbWUiOiJQaWVkbW9udCBIZWFsdGNhcmUiLCJDbGllbnRJZCI6IjcxNGRmNDA2LTg4MDItNDc5Zi1hOTZiLWY0ZTM2MmViYWI3MCIsImV4cCI6MTUzMDIxMjAzMCwiaXNzIjoibG95YWxoZWFsdGguY29tIiwiYXVkIjoibG95YWxoZWFsdGguY29tIn0.nt0JreFFPWOV6Ns1EI0ExWbNBQ_IFW9LzrufibsnbEw"
}
```

### Expiration

Tokens expire after 24 hours. You may request a new token from the `/auth/client/token` endpoint to refresh the client token. Make sure to encrypt the client tokens you store!


### About the API Token

Loyal API uses [JSON Web Tokens](https://jwt.io/introduction/) (JWTs) to authenticating requests.

The scopes claim of this token indicates which actions can be performed with it when calling this API. For example, this token would grant read-only access to users and read/write access to rules. Trying to perform any other action will result in a 403 Forbidden response.
