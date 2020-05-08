---
name: Custom Styling
---

## Custom Styling HTML Attributes

Use the following HTML attributes to configure the styles for total star ratings, subtotal start ratings, and reviews/comments:


### Total Star Ratings
**NOTE:** We highly recommend implementing total star ratings server side for ratings to be effectively crawled and indexed by Google 


```html
<div 
   id=”loyal-totals” 
   data-id=”unique_provider_id”
   data-key=”unique_client_id”
   data-starcolor=”gold”
   data-staroutline=”gray”
   data-width=”100”
   data-textcolor=”gray”
></div>
```

### Subtotal Star Ratings
```html
<div 
   id=”loyal-subtotals” 
   data-id=”unique_provider_id”
   data-key=”unique_client_id”
   data-starcolor=”gold”
   data-staroutline=”gray”
   data-width=”100”
   data-columns=”3”
   data-textcolor=”gray”
></div>
```

### Comments/ Reviews
```html
<div 
   id=”loyal-comments” 
   data-id=”unique_provider_id”
   data-key=”unique_client_id”
   data-starcolor=”gold”
   data-staroutline=”gray”
   data-width=”100”
   data-textcolor=”gray”
   data-readmorecolor=”gray”
   data-limit=”10”
   data-patientname=”<customer> Patient”
></div>
```

#### Required attributes: 
- `id`: necessary to populate each category of ratings data (totals, subtotals, - comments)
- `data-id`: unique provider ID (e.g. NPI, health system ID, CMS ID, etc.)
- `data-key`: unique client public API key  


#### Attribute breakdown and default styles:
- Gray is the default color for the following attributes: `data-starcolor`, `data-staroutline`, `data-textcolor`, `data-readmorecolor`
- Gold is the default color for `data-starcolor`
- If `data-staroutline` is not defined, it will default to `data-textcolor` 
- The width of a star group is defined by `data-width` in pixels
- If `data-columns` is not defined, subtotal categories will display as a stacked list
- `data-readmorecolor` is for styling the “Read More” button displayed at the bottom of a comment list. The color defined affects the button outline, the arrow, and the loader
- `data-limit` defines the number of comments displayed at once. 5 is the default
- `data-patientname` customizes the text displayed at the bottom of each patient comment/review. If not defined, nothing will display
