---
name: Installation
---

## Installation

### Method 1: HTML
```html
<section id=”search”></section>
<script type=”text/javascript” src=”https://connect.loyalhealth.com/client/search.bundle.js” data-id=”search-client-id” data-value=”[Your Client ID]” async>
</script>
```

### Method 2: PUG

Production use  (Pug) Programmatically inject script tag

```pug
section
   #search
 script.
   var cid = '[Your Client ID]';
   var e = !{JSON.stringify(settings.env ? settings.env : "")};
   var s = document.createElement('script');
   s.setAttribute("src","https://connect.loyalhealth.com/client/search.bundle.js")
   s.setAttribute("type","text/javascript")
   s.setAttribute("data-id", "search-client-id")
   s.setAttribute("data-value", cid)
   s.setAttribute("async","")
   document.getElementsByTagName("head")[0].appendChild(s)
```

Development use (Pug)
views/find-care/index.pug

```pug
section
   #search
 script.
   var cid = 'b63bab43-ef1f-4f41-8689-633c5e88d21d';
   var e = !{JSON.stringify(settings.env ? settings.env : "")};
   var s = document.createElement('script');
   var isSearchTest = getParameterByName('searchTest');
   s.setAttribute("src","http://localhost:1234/search.bundle.js")
   if(e === 'development')
     s.setAttribute("src","https://connect-dev.loyalhealth.com/client/search.bundle.js")
   if(e === 'qa')
     s.setAttribute("src","https://connect-qa.loyalhealth.com/client/search.bundle.js")
   if(e === 'demo')
     s.setAttribute("src","https://connect-demo.loyalhealth.com/client/search.bundle.js")
   if(e === 'staging')
     s.setAttribute("src","https://connect-staging.loyalhealth.com/client/search.bundle.js")
   if(isSearchTest)
     s.setAttribute("src","https://connect-test.loyalhealth.com/client/search.bundle.js")
   s.setAttribute("type","text/javascript")
   s.setAttribute("data-id", "search-client-id")
   s.setAttribute("data-value", cid)
   s.setAttribute("async","")
   document.getElementsByTagName("head")[0].appendChild(s)
```

### Route configuration on server

 Search/Scheduling Client will need to add these routes to their route config on their server.  
 `/results`  
 `/provider/:entityId`  
 `/location/:entityId`  
 `/scheduling`  
 `/scheduling/:entityId`  

routes/find-a-physician.js (Node.js)
 
Example: https://loyalhealth.com/find-care/results  
Example 2: https://www.fryemedctr.com/find-a-physician/provider/123456  
 
 These routes will just route back to find-care/index so that the Search client can handle routing on its end.
 Without having these routes on the server side, the server will just throw 404s when Search client routes to these routes.

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



