---
name: Installation
---

## Installation

### Drop HTML and JavaScript

```html
<section id=”search”></section>
<script type=”text/javascript” src=”https://connect.loyalhealth.com/client/search.bundle.js” data-id=”search-client-id” data-value=”[Your Client ID]” async>
</script>
```

### Configure routes on your server

The Search/Scheduling client will need to add these routes to their route config on their server:

 `/results`  
 `/provider/:entityId`  
 `/location/:entityId`  
 `/scheduling`  
 `/scheduling/:entityId`  

These routes will just route back to find-care/index so that the Search client can handle routing on its end. Without having these routes on the server side, the server will just throw 404s when Search client routes to these routes. Here's an example server routing config using `Node.js`:

```js
// Node.js
 
router.get('/results', async function(req, res, next) {
 res.render('find-a-physician/index');
});
 
router.get('/provider/:entityId', async function(req, res, next) {
 res.render('find-a-physician/index');
});
 
router.get('/location/:entityId', async function(req, res, next) {
 res.render('find-a-physician/index');
});
 
router.get('/scheduling', async function(req, res, next) {
 res.render('find-a-physician/index');
});
 
router.get('/scheduling/:entityId', async function(req, res, next) {
 res.render('find-a-physician/index');
});

```
