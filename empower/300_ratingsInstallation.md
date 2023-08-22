---
name: Ratings Installation
---

## Ratings Installation

Adding Transparency to your website is as simple as adding 1 line of JavaScript, 1 HTML tag to the bottom of your HTML inside the <body> tag, and a few HTML attributes. You'll need to replace the `data-key` attribute with a key given to you by our team. Reach out to your Loyal representative if you're not sure where to get this.

Using [the latest version of ReactJS](https://facebook.github.io/react/)

### Provider Totals + Subtotals + Comments

The provider's totals rating component will include: N out of 5 total rating, star rating graphic, the total number of ratings, the total comment count, and all supporting HTML/CSS markup.

The provider’s subtotal rating component will include: N out of 5 rating for each subtotal, star rating graphic for each subtotal, text description for each subtotal, and all supporting HTML/CSS markup.

The provider comments component will include: N out of 5 rating for each comment, star rating graphic, comment text, comment attribution (“Piedmont Patient” in this example), and all supporting HTML/CSS markup.

#### Usage

Be sure to add `<div>` tags inside the `<body>` wherever you want ratings and reviews to display. 

```html
<body>
  <!-- Drop in the Totals component -->
  <div id="loyal-totals" data-id="unique_provider_id" data-key=”unique_client_id”></div>
  <!-- Drop in the Subtotals component -->
  <div id="loyal-subtotals" data-id="unique_provider_id" data-key=”unique_client_id”></div>
  <!-- Drop in the Comments component -->
  <div id="loyal-comments" data-id="unique_provider_id" data-key=”unique_client_id”></div>
  <script
    src="https://empower.loyalhealth.com/clients/universal/empower.bundle.js"
    async
  ></script>
</body>
```
