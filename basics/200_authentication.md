---
name: 'Authentication'
---

## Authentication

Call to the Loyal API will need the `Authorization` HTTP header using the [Bearer authentication scheme](https://tools.ietf.org/html/draft-ietf-oauth-v2-bearer-20#section-2.1).

In order to get your token to pass in your `Authorization` header, you'll first need to make a general `POST` call to our endpoint along with your API Key.

<h3>Get Token <span class="api-badge">POST</span></h3>

`https://api.loyalhealth.com/auth/client/token`

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

Returns a single JSON object of the Authentication, designated from the client's API key

```http
HTTP/1.1 200 OK
{
    "authenticated": true,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy5taWNyb3NvZnQuY29tL3dzLzIwMDgvMDYvaWRlbnRpdHkvY2xhaW1zL3JvbGUiOiJMb3lhbEFwaUNsaWVudEFjY2VzcyIsImh0dHA6Ly9zY2hlbWFzLnhtbHNvYXAub3JnL3dzLzIwMDUvMDUvaWRlbnRpdHkvY2xhaW1zL25hbWUiOiJQaWVkbW9udCBIZWFsdGNhcmUiLCJDbGllbnRJZCI6IjcxNGRmNDA2LTg4MDItNDc5Zi1hOTZiLWY0ZTM2MmViYWI3MCIsImV4cCI6MTUzMDIxMjAzMCwiaXNzIjoibG95YWxoZWFsdGguY29tIiwiYXVkIjoibG95YWxoZWFsdGguY29tIn0.nt0JreFFPWOV6Ns1EI0ExWbNBQ_IFW9LzrufibsnbEw"
}
```
