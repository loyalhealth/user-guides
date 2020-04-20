## Provider Rollups

Aggregate rating for a group of providers

<h3>Get Paged Rollups <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/rollups?offset=X&limit=Y`

```csharp
namespace GetPagedRollup
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var offset = 20; // set the number of rollups to skip
      var limit = 10; // set the number of rollups to retrieve
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/rollups?offset={offset}&limit={limit}";
      var request = new HttpRequestMessage(HttpMethod.Get, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      var response = await HttpClient.SendAsync(request);
      var rollups = JsonConvert.DeserializeObject<IEnumerable<Rollup>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }
  class Rollup
  {
    public bool Active { get; set; }
    public string Description { get; set; }
    public long Id { get; set; }
    public string Name { get; set; }
    public IEnumerable<long> ProviderIds { get; set; }
    public decimal Rating { get; set; }
    public long RatingCount { get; set; }
  }
}
```

```javascript
const request = require('request');
const offset = 20;
const limit = 10;
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/rollups?offset=${offset}&limit=${limit}`,
  headers: { Authorization: `Bearer ${process.env.TOKEN}` }
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Returns a JSON array

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
[
  {
    "active": true,
    "description": "Roll-up of providers related to Cardiology",
    "id": 1,
    "name": "Cardiology",
    "providerIds": ["1013073543", "1063442994", "1134120249", "1174591580", "1316915911"],
    "rating": 4.6,
    "ratingCount": 1888
  },
  {
    "active": false,
    "description": "Roll-up of providers related to Oncology",
    "id": 2,
    "name": "Oncology",
    "providerIds": ["1669474524", "1700923752", "1790754521", "1992817530"],
    "rating": 4.8,
    "ratingCount": 497
  }
]
```

<h3>Get Rollup <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/rollups/:rollupId`

```csharp
namespace GetRollup
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var rollupId = 1; // set your provider id here
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/rollups/{rollupId}";
      var request = new HttpRequestMessage(HttpMethod.Get, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      var response = await HttpClient.SendAsync(request);
      var rollups = JsonConvert.DeserializeObject<Rollup>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }
  class Rollup
  {
    public bool Active { get; set; }
    public string Description { get; set; }
    public long Id { get; set; }
    public string Name { get; set; }
    public IEnumerable<long> ProviderIds { get; set; }
    public decimal Rating { get; set; }
    public long RatingCount { get; set; }
  }
}
```

```javascript
const request = require('request');
const rollupId = 1;
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/rollups/${rollupId}`,
  headers: { Authorization: `Bearer ${process.env.TOKEN}` }
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Returns a JSON object

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "active": true,
  "description": "Roll-up of providers related to Cardiology",
  "id": 1,
  "name": "Cardiology",
  "providerIds": ["1013073543", "1063442994", "1134120249", "1174591580", "1316915911"],
  "rating": 4.6,
  "ratingCount": 1888
}
```
