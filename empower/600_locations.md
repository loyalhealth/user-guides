## Locations

Aggregate rating for a location

<h3>Get Rating and Rating Count for a Location<span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/locations/:locationId`

```csharp
namespace GetLocationRatings
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var locationId = "1234";
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/locations{locationId}/totals";
      var request = new HttpRequestMessage(HttpMethod.Get, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      var response = await HttpClient.SendAsync(request);
      var rollups = JsonConvert.DeserializeObject<IEnumerable<LocationTotals>(await response.Content.ReadAsStringAsync());
    }
  }
  class LocationRating
  {
    public string Id { get; set; }
    public decimal Rating { get; set; }
    public long SurveyCount { get; set; }
  }
}
```

```javascript
const request = require('request');
const locationId = '1234';
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/locations/${locationId}`,
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
{
  "id": "1234",
  "rating": 4.6,
  "surveyCount": 188
}
```

<h3>Get Rating and Rating Count for a Multiple Locations <span class="api-badge">POST</span></h3>

`https://api.loyalhealth.com/empower/location/`

```csharp
namespace GetLocationRatings
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var locationIds = new [] { "1234", "5678" }; // set your location id here
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/locations/totals";
      var request = new HttpRequestMessage(HttpMethod.POST, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      request.Content = new StringContent(JsonConvert.SerializeObject(locationIds));
      var response = await HttpClient.SendAsync(request);
      var rollups = JsonConvert.DeserializeObject<IEnumerable<LocationRating>>(await response.Content.ReadAsStringAsync());
    }
  }
  class LocationRating
  {
    public string Id { get; set; }
    public decimal Rating { get; set; }
    public long SurveyCount { get; set; }
  }
}
```

```javascript
const request = require('request');
const locationIds = ['1234', '5678']; // set your provider ids here;
const options = {
  method: 'POST',
  url: `https://api.loyalhealth.com/empower/locations/totals`,
  headers: { Authorization: `Bearer ${process.env.TOKEN}` },
  body: JSON.stringify(locationIds)
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
[
  {
    "id": "1234",
    "rating": 4.8,
    "surveyCount": 67
  },
  {
    "id": "5678",
    "rating": 4.9,
    "surveyCount": 34
  }
]
```
