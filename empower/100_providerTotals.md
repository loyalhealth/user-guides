---
name: 'Provider Totals'
---

## Provider Totals

Overall ratings for Providers

<h3>Get Total by Provider ID <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/providers/:providerId/totals`

```csharp
namespace GetProviderTotals
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var providerId = "4617"; // set your provider id here
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/providers/{providerId}/totals";
      var totalsRequest = new HttpRequestMessage(HttpMethod.Get, url);
      totalsRequest.Headers.Add("Authorization", $@"Bearer {token}");
      var totalsResponse = await HttpClient.SendAsync(totalsRequest);
      var totals = JsonConvert.DeserializeObject<ProviderTotals>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }

  class ProviderTotals
  {
    public decimal Rating { get; set; }
    public long RatingCount { get; set; }
    public long CommentCount { get; set; }
  }
}
```

```javascript
const request = require('request');
const providerId = '4617'; // set your provider id here;
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/providers/${providerId}/totals`,
  headers: { Authorization: `Bearer ${process.env.TOKEN}` }
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Returns a single JSON object of the Provider, designated from the client's unique provider ID

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "rating": 4.8,
  "ratingCount": 42,
  "reviewCount": 117
}
```

<h3>List Totals by Provider ID <span class="api-badge">POST</span></h3>

`https://api.loyalhealth.com/empower/providers/:providerId/totals`

```csharp
namespace GetProviderTotals
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var providerIds = new [] { "4617", "3142" }; // set your provider id here
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/providers/totals";
      var totalsRequest = new HttpRequestMessage(HttpMethod.Post, url);
      totalsRequest.Headers.Add("Authorization", $@"Bearer {token}");
      totalsRequest.Content = new StringContent(JsonConvert.SerializeObject(providerIds));
      var totalsResponse = await HttpClient.SendAsync(totalsRequest);
      var totals = JsonConvert.DeserializeObject<IEnumerable<ProviderIdWithTotals>>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }
  class ProviderTotals
  {
    public decimal Rating { get; set; }
    public long RatingCount { get; set; }
    public long CommentCount { get; set; }
  }
  class ProviderIdWithTotals
  {
    public string ProviderId { get; set; }
    public ProviderTotals Totals { get; set; }
  }
}
```

```javascript
const request = require('request');
const providerIds = ['4617', '3142']; // set your provider ids here;
const options = {
  method: 'POST',
  url: 'https://api.loyalhealth.com/empower/providers/totals',
  headers: { Authorization: `Bearer ${process.env.TOKEN}` },
  body: JSON.stringify(providerIds)
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Post an array of id's to the request body. Returns JSON list of Totals based on the provider id's given. Recommend using Postman to send data requests here for testing.

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
[
  {
    "providerId": "4617",
    "totals": {
      "rating": 4.7,
      "ratingCount": 8,
      "reviewCount": 0
    }
  },
  {
    "providerId": "3142",
    "totals": {
      "rating": 4.8,
      "ratingCount": 68,
      "reviewCount": 110
    }
  }
]
```
