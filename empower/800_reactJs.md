## ReactJS

Using [the latest version of ReactJS](https://facebook.github.io/react/)

### Provider Totals + Subtotals + Comments

The provider's totals rating component will include: N out of 5 total rating, star rating graphic, the total number of ratings, the total comment count, and all supporting HTML/CSS markup.

The provider’s subtotal rating component will include: N out of 5 rating for each subtotal, star rating graphic for each subtotal, text description for each subtotal, and all supporting HTML/CSS markup.

The provider comments component will include: N out of 5 rating for each comment, star rating graphic, comment text, comment attribution (“Piedmont Patient” in this example), and all supporting HTML/CSS markup.

#### Usage

```html
<head>
  <!-- other <head> tags -->
  <link href="https://empower.loyalhealth.com/clients/[your-client-name]/empower.bundle.css" rel="stylesheet" type="text/css" />
</head>
<body>
  <!-- Drop in the Totals component -->
  <div id="loyal-totals"></div>
  <!-- Drop in the Subtotals component -->
  <div id="loyal-subtotals"></div>
  <!-- Drop in the Comments component -->
  <div id="loyal-comments"></div>
  <script src="https://empower.loyalhealth.com/clients/[your-client-name]/empower.bundle.js" async></script>
</body>
```
