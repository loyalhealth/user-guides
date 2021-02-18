---
name: 'Shadow DOM'
---

## Shadow DOM

Guide is encapsulated in a [Shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM) element to prevent CSS conflicts with clients' existing stylesheets. To access html elements within Guide, you'll need to query `window.guideShadowRoot` instead of `document`.