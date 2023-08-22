---
name: Web Scheduling Installation
---

## Web Scheduling Installation

### Drop HTML and JavaScript

To use the Web Scheduling module, this block of code should be placed on the page where the module should appear (e.g. between the header and footer). When the script below loads, it finds the appropriate section in the dom and creates a shadowRoot where the search module will live. The `script` tag **must** come after the `section` tag.


```html
<section id=”search”></section>
<script type=”text/javascript” src=”https://scheduling.loyalhealth.com/client/scheduling.bundle.js” data-id=”search-client-id” data-value=”[Your Client ID]” async>
</script>
```

### Configure routes on your server

These routes need to be set up to redirect to the same page where the search module is loading:

`[your root url]/:npi`

The scheduling root url is configured through our settings portal.

Example in `node.js` where the root url is `book-appointment`:

```js
// Node.js
 
router.get('book-appointment/:npi', function(req, res, next) {
 res.render('loyal-scheduling/index');
})
```

We recommend that you disable loyal’s guide solution on the scheduling page so that users are not distracted by the chatbot while they schedule. 

### FAQ

Q: We need to set up a beta/staging site to test on first

A: The only change for your beta/staging site from the above install instructions will be changing the src on the script tag to "https://scheduling-staging.loyalhealth.com/client/scheduling.bundle.js" and you will need to make sure you’ve got your loyal staging environment set up to point to your EHR staging environment.

-
Q: We have a content security policy that isn’t allowing your script to load.

A: You will need to update your content security policy to allow data from *.loyalhealth.com.

Example:
```html
<meta
  http-equiv="Content-Security-Policy"
  content="
    default-src 'self' 'unsafe-eval' *.loyalhealth.com;
    style-src 'self' 'unsafe-inline';
    connect-src 'self' *.loyalhealth.com;
    img-src * data:; 
  "
/>
```

--
Q: What if I have global event listeners that stop propagation of events? For example, I want to intercept space bar presses to make the scrolling of the page smoother, but now putting spaces in the search bar isn't working?

A: We use the shadow dom, which means at the document level any event's target will be the section we drop our module into. If you're setting up global event listeners where events need to be intercepted unless the target of the event is the input or something similar, you'll need to look at the composed path instead of the event's target i.e. event.composedPath[0] would be the actual target of the event.

--
Q: What if I need to use a query param for the npi instead of having it be part of the url?

A: The query param must be named npi (e.g. `myhealthcaresystem.com/book-appointment?npi=123456789`), and you would change your routing to the below:

This route needs to be set up to redirect to the same page where the scheduling module is loading:
`[your root url]`

The scheduling root url is configured through our settings portal.

Example in node.js where the root url is book-appointment:
```js
// Node.js

router.get('book-appointment', function(req, res, next) {
 res.render('loyal-scheduling/index');
})
```

