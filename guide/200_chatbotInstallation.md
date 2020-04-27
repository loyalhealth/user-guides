---
name: 'Chatbot Installation Test'
---

## Chatbot Installation

Adding Guide to your website is as simple as adding 1 line of JavaScript and 1 HTML tag to the bottom of your HTML inside the `<body>` tag. You'll need to replace the `data-value` attribute with a key given to you by our team. Reach out to your Loyal representative if you're not sure where to get this.

```html
<div id="guide"></div>
<script src="https://guide.loyalhealth.com/client/client.bundle.js" data-id="guide-client-id" data-value="[your-unique-client-id]" async></script>
```

<p class="warning">
  IMPORTANT: Some browsers, IE10 and IE9 are probably the two most relevant, do not support TLS 1.2. If your site is still supporting these browsers, you will need to exclude Guide with IE conditionals:
</p>

```html
<!--[if lt IE 11]>
  dont add Guide's javascript ELSE add Guide!
<![endif]-->
```
