---
name: 'JavaScript API'
---

## JavaScript API

To get more out of Guide, you can use our JavaScript API to do all sorts of useful things, like updating the padding of the positioning or creating custom class names to conduct A/B tests.

The Guide team is continuing to update what settings can be controlled. Right now we offer only 2 things:

| Index | Key              | Example Value  | Description                                                                                                                                            |
| ----- | ---------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1     | padding          | 25             | Integer: A number that will define the "padding" around the Guide launcher/widget                                                                      |
| 2     | customClassName  | 'scranton-bot' | String: A value that will be added to the top level of the React component, allowing the client to run A/B tests or add custom CSS styles              |
| 3     | disableShadowDOM | false          | Boolean: Disables the Shadow DOM encapsulation to allow the client to apply custom CSS styles to Guide. (This may cause unintended styling collisions) |

```html
<-- add a script tag in your head to customize your Guide implementation -->
<script>
  window.guideSettings = {
    padding: 25,
    customClassName: 'scranton-bot',
    disableShadowDOM: false
  };
</script>
```
