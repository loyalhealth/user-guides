---
name: A/B Testing
---

## A/B Testing

Many times you'll want to run an A/B test for certain designs to see if Guide can be optimized. We recommend using Google Analytics and their Tag Manager tool to help you establish this approach.

An easy way to do this would be to randomize between 0 and 1, and then add some CSS class to our `guideSettings` object - depending on if the value is 0 or 1. You can then push this to the `dataLayer` object and let Google handle it from there.

```html
<script>
  window.guideSettings = {
    padding: 25,
    customClassName: 'scranton-bot'
  };
  var random = Math.round(Math.random());
  if (random === 0) {
    window.guideSettings.customClassName = 'custom-ab-test-class';
    window.dataLayer = window.dataLayer || [];
    window.dataLayer.push({
      event: 'custom-ab-test-class'
    });
  }
</script>
```
