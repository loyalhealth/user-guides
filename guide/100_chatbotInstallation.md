---
name: 'Chatbot Installation'
---

## Chatbot Installation
### Method 1: Javascript 
Adding Guide to your website is as simple as adding 1 line of JavaScript and 1 HTML tag to the bottom of your HTML inside the `<body>` tag. You'll need to replace the `data-value` attribute with a key given to you by our team. Reach out to your Loyal representative if you're not sure where to get this.

```html
<div id="guide"></div>
<script src="https://guide.loyalhealth.com/client/client.bundle.js" data-id="guide-client-id" data-value="[your-unique-client-id]" async></script>
```

<p class="warning">
  IMPORTANT: Guide is not supported on deprecated browsers (e.g. IE10 and earlier). If your site is still supporting these browsers, Guide will be automatically disabled in these environments.
</p>

### Method 2: Google Tag Manager
You can also install Guide using Google Tag Manager. You’ll simply need to add the code snippet below to add Guide to your GTM account:
```
var g = document.createElement('script');
g.setAttribute('src', 'https://guide.loyalhealth.com/client/client.bundle.js');
g.setAttribute('type', 'text/javascript');
g.setAttribute('data-id', 'guide-client-id');
g.setAttribute('data-value', 'YOUR-UNIQUE-CLIENT-ID');
g.setAttribute('async', 'async');
document.getElementsByTagName('head')[0].appendChild(g);
```
