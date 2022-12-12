---
name: Touchpoint Surveys Setup
---

## Installation and Usage

To host Touchpoint Surveys you will need to include our client script and 
configure it to render to the DOM element of your choosing.

### Installation

Be sure to add `<div>` tags inside the `<body>` wherever you want ratings and 
reviews to display.

```html
<body>
  <!-- Provide an empty element we will render into -->
  <div id="my-survey-container"></div>
  
  
  <!-- Inject the touchpoint survey script to the bottom of the body tag -->
  <script
    src="https://empower.loyalhealth.com/client/empower-survey.bundle.js"
    data-loyal-client-id="<<your client id>>"
    data-loyal-container-id="my-survey-container"
  ></script>
</body>
```

### Usage

After installation, you can configure your surveys in the admin to use the 
URL that has the script loaded and configured. 