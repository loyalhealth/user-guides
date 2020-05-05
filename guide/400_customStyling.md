---
name: 'Custom Styling'
---

## Custom Styling

### Enabling Custom Styles

By default, we wrap Guide in a Shadow DOM element. You'll need to disable this in order to apply custom CSS styles (see above). Be aware that this may cause unintended CSS styling conflicts with any base styles on the page.

### Classname Matching

We use [styled-components](https://www.styled-components.com/docs) for styling Guide in React. Since styled-components creates dynamic class names each time the app is built, it's unreliable to reference specific class names like `Header__HeaderWrapper-ej9zxe-0`, since the hash value will change often. Instead, you can use [substring matching](https://www.w3.org/TR/selectors/#attribute-substrings) to access the specific class via its component name (`Header__HeaderWrapper` in the example above), which is less likely to change.

For example, if you're attempting to style the following element

```html
<div class="Header__HeaderWrapper-ej9zxe-0">
  This is the header
</div>
```

you would use

```css
div[class^="Header__HeaderWrapper"] {
  <<custom styles here>>
}
```

instead of

```css
.Header__HeaderWrapper-ej9zxe-0 {
  <<this would not work if the app was rebuilt>>
}
```
