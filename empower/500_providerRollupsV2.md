## Provider Rollups V2

Aggregate rating for a group of providers

<h3>Get Paged Rollups <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/v2/rollups?offset=X&limit=Y`

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
      var url = $"https://api.loyalhealth.com/empower/v2/rollups?offset={offset}&limit={limit}";
      var request = new HttpRequestMessage(HttpMethod.Get, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      var response = await HttpClient.SendAsync(request);
      var rollups = JsonConvert.DeserializeObject<IEnumerable<Rollup>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }

  class Subtotal
  {
    public string Description { get; set; }
    public decimal Rating { get; set; }
  }

  class Comment
  {
    public string Comment { get; set; }
    public string Question { get; set; }
  }

  class Review
  {
    public IEnumerable<Comment> { get; set; }
    public decimal Rating { get; set; }
    public DateTime SurveyDate { get; set;}
    public string ProviderId { get; set; }
  }

  class Rollup
  {
    public long Id { get; set; }
    public string Description { get; set; }
    public string Name { get; set; }
    public IEnumerable<string> ProviderIds { get; set; }
    public decimal Rating { get; set; }
    public long RatingCount { get; set; }
    public long ReviewCount { get; set; }
    public IEnumerable<Subtotal> Subtotals { get; set; }
    public IEnumerable<Review> Reviews { get; set; }
  }
}
```

```javascript
const request = require('request');
const offset = 20;
const limit = 10;
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/v2/rollups?offset=${offset}&limit=${limit}`,
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
    "description": "Roll-up of providers related to Cardiology",
    "id": 1,
    "name": "Cardiology",
    "providerIds": ["1013073543", "1063442994", "1134120249", "1174591580", "1316915911"],
    "rating": 4.6,
    "ratingCount": 1888,
    "reviewCount": 200,
    "subtotals": [
      {
        "description": "Friendliness/courtesy",
        "rating": 4.9
      },
      {
        "description": "Explanations about your problem/condition",
        "rating": 4.8
      }
    ],
    "reviews": []
  },
  {
    "description": "Roll-up of providers related to Oncology",
    "id": 2,
    "name": "Oncology",
    "providerIds": ["1669474524", "1700923752", "1790754521", "1992817530"],
    "rating": 4.8,
    "ratingCount": 497,
    "reviewCount": 200,
    "subtotals": [
      {
        "description": "Friendliness/courtesy",
        "rating": 4.9
      },
      {
        "description": "Explanations about your problem/condition",
        "rating": 4.8
      }
    ],
    "reviews": []
  }
]
```

<h3>Get Rollup <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/v2/rollups/:rollupId`

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
      var url = $"https://api.loyalhealth.com/empower/v2/rollups/{rollupId}";
      var request = new HttpRequestMessage(HttpMethod.Get, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      var response = await HttpClient.SendAsync(request);
      var rollups = JsonConvert.DeserializeObject<Rollup>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }

  class Subtotal
  {
    public string Description { get; set; }
    public decimal Rating { get; set; }
  }

  class Comment
  {
    public string Comment { get; set; }
    public string Question { get; set; }
  }

  class Review
  {
    public IEnumerable<Comment> { get; set; }
    public decimal Rating { get; set; }
    public DateTime SurveyDate { get; set;}
    public string ProviderId { get; set; }
  }

  class Rollup
  {
    public long Id { get; set; }
    public string Description { get; set; }
    public string Name { get; set; }
    public IEnumerable<string> ProviderIds { get; set; }
    public decimal Rating { get; set; }
    public long RatingCount { get; set; }
    public long ReviewCount { get; set; }
    public IEnumerable<Subtotal> Subtotals { get; set; }
    public IEnumerable<Review> Reviews { get; set; }
  }
}
```

```javascript
const request = require('request');
const rollupId = 1;
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/v2/rollups/${rollupId}`,
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
  "description": "Roll-up of providers related to Cardiology",
  "id": 1,
  "name": "Cardiology",
  "providerIds": ["1013073543", "1063442994", "1134120249", "1174591580", "1316915911"],
  "rating": 4.6,
  "ratingCount": 1888,
  "reviewCount": 200,
  "subtotals": [
    {
      "description": "Friendliness/courtesy",
      "rating": 4.9
    },
    {
      "description": "Explanations about your problem/condition",
      "rating": 4.8
    }
  ],
  "reviews": []
}
```

<h3>Get Rollup and Reviews<span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/v2/rollups/:rollupId/reviews?offset=X&limit=Y`

```csharp
namespace GetRollup
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var offset = 0;
      var limit = 2;
      var rollupId = 1; // set your rollup id here
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/v2/rollups/{rollupId}/reviews?offset={offset}&limit={limit}";
      var request = new HttpRequestMessage(HttpMethod.Get, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      var response = await HttpClient.SendAsync(request);
      var rollups = JsonConvert.DeserializeObject<Rollup>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }

  class Subtotal
  {
    public string Description { get; set; }
    public decimal Rating { get; set; }
  }

  class Comment
  {
    public string Comment { get; set; }
    public string Question { get; set; }
  }

  class Review
  {
    public IEnumerable<Comment> { get; set; }
    public decimal Rating { get; set; }
    public DateTime SurveyDate { get; set;}
    public string ProviderId { get; set; }
  }

  class Rollup
  {
    public long Id { get; set; }
    public string Description { get; set; }
    public string Name { get; set; }
    public IEnumerable<string> ProviderIds { get; set; }
    public decimal Rating { get; set; }
    public long RatingCount { get; set; }
    public long ReviewCount { get; set; }
    public IEnumerable<Subtotal> Subtotals { get; set; }
    public IEnumerable<Review> Reviews { get; set; }
  }
}
```

```javascript
const request = require('request');
const offset = 0;
const limit = 2;
const rollupId = 1;
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/v2/rollups/${rollupId}/reviews?offset=${offset}&limit=${limit}`,
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
  "description": "Roll-up of providers related to Cardiology",
  "id": 1,
  "name": "Cardiology",
  "providerIds": ["1013073543", "1063442994", "1134120249", "1174591580", "1316915911"],
  "rating": 4.6,
  "ratingCount": 1888,
  "reviewCount": 200,
  "subtotals": [
    {
      "description": "Friendliness/courtesy",
      "rating": 4.9
    },
    {
      "description": "Explanations about your problem/condition",
      "rating": 4.8
    }
  ],
  "reviews": [
    {
      "comments": [
        {
          "comment": "Comment text would be here",
          "question": "Question text would be here (if available)"
        },
        {
          "comment": "Comment text would be here",
          "question": "Question text would be here (if available)"
        }
      ],
      "rating": 5.0,
      "surveyDate": "2019-09-26T00:00:00",
      "providerId": "1508845512"
    }
  ]
}
```
