## Provider Surveys

Surveys for Providers

<h3>Get Surveys <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/empower/providers/:providerId/surveys`

```csharp
namespace GetProviderSurveys
{
  class Program
  {
    private static readonly HttpClient HttpClient = new HttpClient();
    static async Task Main(string[] args)
    {
      var providerId = "4617"; // set your provider id here
      var token = TOKEN; // see documentation on how to get this at the top of this page
      var url = $"https://api.loyalhealth.com/empower/providers/{providerId}/surveys";
      var request = new HttpRequestMessage(HttpMethod.Get, url);
      request.Headers.Add("Authorization", $@"Bearer {token}");
      var response = await HttpClient.SendAsync(request);
      var subtotals = JsonConvert.DeserializeObject<IEnumerable<Survey>>(await totalsResponse.Content.ReadAsStringAsync());
    }
  }
  class Comment
  {
    public string CommentText { get; set; }
    public string Question { get; set; }
  }
  class Survey
  {
    public IEnumerable<Comment> Comments { get; set; }
    public decimal Rating { get; set; }
    public DateTime SurveyDate { get; set; }
  }
}
```

```javascript
const request = require('request');
const providerId = '4617'; // set your provider id here;
const options = {
  method: 'GET',
  url: `https://api.loyalhealth.com/empower/providers/${providerId}/surveys`,
  headers: { Authorization: `Bearer ${process.env.TOKEN}` }
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Returns a JSON array of all the Provider Surveys

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
[
  {
    "comments": [
      {
        "comment": "Excellent care from the doctor and his staff",
        "question": "Was there anything you feel was exceptional?"
      },
      {
        "comment": "I had to wait over an hour to be seen",
        "question": "Was there anything you feel could be improved?"
      }
    ],
    "rating": 5,
    "surveyDate": "2017-07-31T00:00:00"
  },
  {
    "comments": [
      {
        "comment": "I feel as though I got the best care possible & feel blessed that Dr Giaski was my surgeon.",
        "question": ""
      }
    ],
    "rating": 5,
    "surveyDate": "2017-05-19T00:00:00"
  }
]
```
