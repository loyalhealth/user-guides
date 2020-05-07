---
name: 'Page Takeover'
---
## Page Takeover
Enabling a Page Takeover for Guide will give you the ability to open Guide from a link. This is useful if you want to direct consumers to use the tool for a specific reason or focus the consumer on a specific use case within your chatbot.

In order to set up the page takeover, all you need to do is create a specific URL, add any desired styling (page title, introduction, etc.) to the page and add the same Guide code snippet used elsewhere on your site to the URL. You can then use that URL as a link to open Guide throughout your site. 

Note: if you already have Guide enabled sitewide, the standard widget will not appear on the page you have designated as your takeover page so that Guide only appears once.

**Customer Example - Baptist Health South Florida Coronavirus Risk Assessment**:
![pagetakeoverbhsf](https://raw.githubusercontent.com/loyalhealth/user-guides/master/images/pagetakeoverbhsf.jpg "Guide Desktop View Expanded")

Instructions:
1. Configure URL for page takeover and provide that URL to the Loyal team
2. Add the standard Guide code snippet to the page (the bot will render wherever you put the `<div id="guide"></div>` element)
3. You can add your own css class to that element to determine the width/height of the bot and set specific dimensions for the #guide root element
4. Take the div element out of the global injection and only add it to that specific page. our app creates the root element on startup it if it doesn’t exist.
