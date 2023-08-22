---
name: Care Search Installation
---

## Care Search Installation

### Drop HTML and JavaScript

To use the Care Search module, this block of code should be placed on the page where the module should appear (e.g. between the header and footer). When the script below loads, it finds the appropriate section in the dom and creates a shadowRoot where the search module will live. The `script` tag **must** come after the `section` tag.


```html
<section id=”search”></section>
<script type=”text/javascript” src=”https://connect.loyalhealth.com/client/search.bundle.js” data-id=”search-client-id” data-value=”[Your Client ID]” async>
</script>
```

### Configure routes on your server

These routes need to be set up to redirect to the same page where the search module is loading:

`[your root url]`

`[your root url]/results`

`[your root url]/provider/:entityId`

`[your root url]/location/:entityId`
 
The search module leverages client-side routing, so if any of the routes are missing and a user hits a results/provider/location link directly, your routes may redirect them to a page not found error. Alternatively, if it works better with your site's routing, instead of enumerating the routes, you could do an inclusive route such as `find-care/*`

Example in `node.js` where the root url is `find-care`:

```js
// Node.js
 
router.get('/find-care', async function(req, res, next) {
 res.render('find-a-physician/index');
});
 
router.get('find-care/results', async function(req, res, next) {
 res.render('find-a-physician/index');
});
 
router.get('find-care/provider/:entityId', async function(req, res, next) {
 res.render('find-a-physician/index');
});
 
router.get('find-care/location/:entityId', async function(req, res, next) {
 res.render('find-a-physician/index');
});
```

### FAQ

Q: What if I want to use a different url when testing this than I will be when it goes live? For example, I’d like to host the test page at myhealthcaresystem.com/test-search but when it goes live we’ll be at myhealthcaresystem.com/find-care.

A: If you add an attribute to the script: data-loyal-search-qa-root-url=”test-search” then this will override the root url that you have set up in the settings. WARNING: only put this attribute on your script tag in your test page. If you leave it there for the production page, your routing will not work properly.

---

Q: What if I have global event listeners that stop propagation of events? For example, I want to intercept space bar presses to make the scrolling of the page smoother, but now putting spaces in the search bar isn't working?

A: We use the shadow dom, which means at the document level any event's target will be the section we drop our module into. If you're setting up global event listeners where events need to be intercepted unless the target of the event is the input or something similar, you'll need to look at the composed path instead of the event's target i.e. event.composedPath[0] would be the actual target of the event.

---

Q: What about z-indexes? Things don't seem to be stacking right with the footer?

A: We will create a new css stacking context at the root level where our section is defined. Nothing inside will go overtop of your headers, but if the footers come in the dom afterwards, we could end up being either on top of the footer with things like the typeahead, or below the footer with the typeahead. If your footer doesn't do anything to create a new stacking context or raise itself up in the stacking context, the typeahead will lay over the footer as expected.

---

Q: When do I need the profile Id?

A: Profile Id isn’t needed if you only have a single profile for your market. If you want to use anything other than the default profile, you will need to include profile Id.
