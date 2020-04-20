## Provider Subtotals

Subtotals (also known as Rated Sections) for Providers

<h3> Get Subtotals <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/providers/:providerId/subtotals`

```csharp
namespace GetProviderSubtotals
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var providerId = "4617"; // set your provider id here
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/providers/{providerId}/subtotals";
      var request = new HttpRequestMessage(HttpMethod.Get, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      var response = await HttpClient.SendAsync(request);
      var subtotals = JsonConvert.DeserializeObject<IEnumerable<ProviderSubtotals>>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }

  class ProviderSubtotals
  {
    public string Description { get; set; }
    public decimal Rating { get; set; }
  }
}
```

```javascript
const request = require('request');
const providerId = '4617'; // set your provider id here;
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/providers/${providerId}/subtotals`,
  headers: { Authorization: `Bearer ${process.env.TOKEN}` }
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Returns a JSON array of all the Provider Subtotals

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
[
  {
    "description": "Friendliness/courtesy",
    "rating": 4.9
  },
  {
    "description": "Explanations about your problem/condition",
    "rating": 4.9
  },
  {
    "description": "Used words you could understand",
    "rating": 4.9
  },
  {
    "description": "Likelihood of recommending to others",
    "rating": 4.9
  }
]
```
