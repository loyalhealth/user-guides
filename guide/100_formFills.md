---
name: 'Form Fills'
---

## Form Fills

Form fill data captured by Guide bot

<h3>Get Form Fill Descriptions <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/guide/v1/:clientId/formfills/descriptions/all`

```csharp
namespace FormFillExample
{
  class FormFillDescriptionExample
  {
     private static readonly HttpClient HttpClient = new HttpClient();
     static async Task<List<FormFillDescription>> GetFormFillDescriptionsAsync(string clientId, string token)
     {
            var url = $@"https://api.loyalhealth.com/guide/v1/{clientId}/formfills/descriptions/all";
            var ffdRequest = new HttpRequestMessage(HttpMethod.Get, url);
            ffdRequest.Headers.Add("Authorization", $@"Bearer {token}");
            var ffdResponse = await HttpClient.SendAsync(ffdRequest);
            var responsestring = await ffdResponse.Content.ReadAsStringAsync();
            var descriptions = JsonConvert.DeserializeObject<List<FormFillDescription>>(responsestring);
            return descriptions;
     }
  }

  public class FormFillDescription
  {
        public int Id { get; set; }
        public string Description { get; set; }
  }
}
```

```javascript
const request = require('request');
const { clientId } = require('ids');
const options = {
  method: 'GET',
  `https://api.loyalhealth.com/guide/v1/${clientId}/formfills/descriptions/all`
  headers: { 'Authorization': `Bearer ${process.env.TOKEN}` }
}

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Returns a list of JSON objects with form fill id and description

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
[
  {
    "id": 1,
    "description": "Newsletter Signup"
  },
  {
    "id": 2,
    "description": "Schedule an Appointment"
  }
]
```

<h3>Get Unreviewed Form Fills <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/guide/v1/:clientId/formfills/unreviewed/:descriptionId`

```csharp
namespace FormFillExample
{
  class FormFillDescriptionExample
  {
     private static readonly HttpClient HttpClient = new HttpClient();
     static async Task<List<FormFill>> GetUnreviewedFormFillsAsync(string clientId, string token, int descriptionId, int offset, int count)
        {
            var url = $@"https://api.loyalhealth.com/guide/v1/{clientId}/formfills/unreviewed/{descriptionId}/?offset={offset}&count={count}";
            var ffdRequest = new HttpRequestMessage(HttpMethod.Get, url);
            ffdRequest.Headers.Add("Authorization", $@"Bearer {token}");
            var ffdResponse = await HttpClient.SendAsync(ffdRequest);
            var responsestring = await ffdResponse.Content.ReadAsStringAsync();
            var formFills = JsonConvert.DeserializeObject<List<FormFill>>(responsestring);
            return formFills;
        }
  }

  public class FormFill
	{
		public int Id { get; set; }
		public string Description { get; set; }
		public int DescriptionId { get; set; }
		public string ConversationId { get; set; }
		public DateTime CreationDateTime {get; set; }
		public bool Reviewed { get; set; }
		public string ReviewedBy { get; set; }
		public DateTime? ReviewDateTime { get; set; }
		public List<FormFillDetail>  Details{ get; set; }
	}

  public class FormFillDetail
	{
		public int Id { get; set; }
		public int FormFillId { get; set; }
		public string VariableName { get; set; }
		public string VariableValue { get; set; }
	}
}
```

```javascript
const request = require('request');
const { clientId, descriptionId } = require('ids');
const offset = 20;
const count = 10;
const options = {
  method: 'GET',
  `https://api.loyalhealth.com/guide/v1/${clientId}/formfills/unreviewed/${descriptionId}/?offset=${offset}&count=${count}`,
  headers: { 'Authorization': `Bearer ${process.env.TOKEN}` }
}

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Returns an array of JSON objects with form fill data

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
[
  {
    "id": 48,
    "description": "Schedule an Appointment",
    "descriptionId": 2,
    "conversationId": "7fcf75160e6943738178388a557f3928",
    "creationDateTime": "2018-04-12T17:05:45.04",
    "reviewed": false,
    "details": [
      {
        "id": 168,
        "formFillId": 48,
        "variableName": "custom_first_name",
        "variableValue": "garry"
      }
    ]
  }
]
```

<h3>Mark Form Fill As Reviewed <span class="api-badge">GET</span></h3>

`https://api.loyalhealth.com/guide/v1/:clientId/formfills/reviewed/:formFillId`

```csharp
namespace FormFillExample
{
  class FormFillDescriptionExample
  {
      private static readonly HttpClient HttpClient = new HttpClient();
      static async Task MarkFormFillAsReviewedAsync(string clientId, string token, int formFillId)
      {
            var url = $@"https://api.loyalhealth.com/guide/v1/{clientId}/formfills/review/{formFillId}";
            var ffdRequest = new HttpRequestMessage(HttpMethod.Post, url);
            ffdRequest.Headers.Add("Authorization", $@"Bearer {token}");
            var ffdResponse = await HttpClient.SendAsync(ffdRequest);
      }
  }
}
```

```javascript
const request = require('request');
const { clientId, formFillId } = require('ids');
const options = {
  method: 'POST',
  url: `https://api.loyalhealth.com/guide/v1/${clientId}/formfills/review/${formFillId}`,
  headers: { Authorization: `Bearer ${process.env.TOKEN}` }
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body);
  }
}
request(options, callback);
```

Returns a HTTP response with status 200

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
