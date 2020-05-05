---
name: 'Shadow DOM'
---

## Shadow DOM

Guide is encapsulated in a [shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM) element to prevent CSS conflicts with clients' existing stylesheets. To access html elements within Guide, you'll need to query `window.guideShadowRoot` instead of `document`. If you want to add custom CSS styles for Guide, you'll need to disable the Shadow DOM encapsulation by setting `disableShadowDOM` to `true` in the `window.guideSettings` object.
