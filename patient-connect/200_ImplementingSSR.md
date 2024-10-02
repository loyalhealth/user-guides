---
name: Implementing Server-Side Rendering (SSR) for Provider and Location Profile Pages (WIP 🚧)
---

# Implementing Server-Side Rendering (SSR) for Provider and Location Profile Pages (WIP 🚧)

## Introduction
**The Server-Side Rendering (SSR)** feature in Care Search is an optional enhancement that allows provider and location information to be included in the initial HTML response from your server. This improves the chances that search engines will index your profile pages correctly, as key content is included at the time of page load.

> **Note: While SSR can help with SEO, many other factors (e.g., page speed, mobile-friendliness) influence SEO performance.**

## Why Use SSR?
By default, Care Search uses JavaScript to fetch and render location and provider information after the page has already loaded. This may not be ideal for search engines, which prefer to see all key content when the page first loads. SSR allows your server to insert the provider or location data directly into the HTML before it’s sent to the user’s browser.

## How SSR Works
- **Client-Side Rendering**: Normally, Care Search renders profile or location information by calling APIs from the browser **after** the page has loaded, and inserting the data into the `<section id="loyal-search"></section>` tag.
- **Server-Side Rendering**: With SSR, you can make a server-side request to the SSR API to fetch the HTML for provider or location data **before** responding to the client. This pre-fetched content is inserted into the `#loyal-search` section in the HTML response.

## Client-Side Rendering Fallback
It’s highly recommended to keep the `https://connect.loyalhealth.com/client/search.bundle.js` script tag on the page, even when using SSR. In case the SSR request fails, the client-side rendering will execute as usual, ensuring that provider and location data still appear on the page.

## Implementing SSR
Normally, your site’s page for a provider or location would include an empty placeholder like this:
```html
<section id="loyal-search"></section>
```
With SSR, when your server receives a request for a provider or location page (e.g., `/find-care/provider/:entityId` or `/find-care/location/:entityId`), instead of returning the page with an empty `<section>`, it should call our SSR API to pre-load content:
```
GET https://api.loyalhealth.com/search-ssr/:clientId/:marketId/:profileId?/:entityType/profile/:entityId
```
- `clientId`: Your unique client ID.
- `marketId`: Your market ID.
- `profileId`: (Optional) The profile ID, if you're using a non-default profile.
- `entityType`: Either `provider` or `location`, depending on the type of data you are fetching.
- `entityId`: The ID of the provider or location.
  
The API will return a chunk of HTML that can be inserted into the `#loyal-search` section before sending the page back to the user’s browser.

## Examples
Below are examples of how to do this in different server-side environments.

### Node.js (Express)
```js
const express = require('express');
const axios = require('axios');
const app = express();

app.get('/find-care/:entityType/:entityId', async (req, res) => {
  const { entityId, entityType } = req.params;
  const clientId = 'your-client-id';
  const marketId = 'your-market-id';
  
  var ssrHtml = '';
  try {
    // Fetch SSR HTML for the provider or location
    const response = await axios.get(`https://api.loyalhealth.com/search-ssr/${clientId}/${marketId}/${entityType}/profile/${entityId}`);
    ssrHtml = response.data;
  } catch(error) {
    console.error('Error fetching SSR content', error);
  }

    // Insert the SSR HTML into the page
    const htmlPage = `
      <html>
      <body>
        <section id="loyal-search">
          ${ssrHtml}
        </section>
        <script src="https://connect.loyalhealth.com/client/search.bundle.js" data-loyal-client-id="${clientId}" data-loyal-market-id="${marketId}"></script>
      </body>
      </html>
    `;

    res.send(htmlPage);
});
```
In this example, the SSR HTML is fetched and inserted into the `#loyal-search` section before returning the full HTML response to the client.

### WordPress (PHP)
If your website is built using WordPress, you can integrate SSR for provider and location pages by dynamically fetching the `entity_id` and `entity_type` from the URL. This example uses a WordPress **shortcode** to call the Care Search SSR API and insert the returned HTML directly into your pages. To implement SSR, you’ll need to add some PHP code to your WordPress site. You can place this code in your theme’s `functions.php` file or a custom plugin.

```php
// Function to fetch SSR content from the Care Search API
function get_ssr_profile_content($entity_id, $entity_type) {
    $client_id = 'your-client-id';  // Replace with your client ID
    $market_id = 'your-market-id';  // Replace with your market ID
    
    // Construct the SSR API URL
    $api_url = "https://api.loyalhealth.com/search-ssr/$client_id/$market_id/$entity_type/profile/$entity_id";
    
    // Make the request to the SSR API
    $response = wp_remote_get($api_url);

    if (is_wp_error($response)) {
        return '';
    }

    $body = wp_remote_retrieve_body($response);
    
    return $body;
}

// Function to extract entity_id and entity_type from the current URL
function get_current_entity_id() {
    global $wp;
    
    // Get the current URL path
    $current_url = home_url($wp->request);
    
    // Extract entity_id and entity_type from the URL (e.g., /find-care/provider/0123456789)
    if (preg_match('/find-care\/(provider|location)\/(\d+)/', $current_url, $matches)) {
        return array(
            'entity_type' => $matches[1],  // 'provider' or 'location'
            'entity_id' => $matches[2]     // The id
        );
    }
    
    return null;
}

// Shortcode to display SSR content
add_shortcode('ssr_profile_content', 'display_ssr_profile_content');
function display_ssr_profile_content() {
    $entity_info = get_current_entity_id();

    if (!$entity_info) {
        return '';
    }

    // Fetch and return the SSR content using the extracted values
    return get_ssr_profile_content($entity_info['entity_id'], $entity_info['entity_type']);
}
```
In this example, the shortcode `[ssr_profile_content]` is defined which can be placed in the desired wordpress page and will automatically insert SSR content.

## Post-SSR Implementation: Updating Care Search Settings

Once SSR has been successfully implemented on the server, the final step is to toggle a flag in the Care Search settings. This ensures that the Care Search script recognizes SSR is now active.

### Why Is This Step Important?
In scenarios where Care Search is still relying on CSR (Client-Side Rendering) — for instance, on the search results page — when a user clicks on a result, the profile will be displayed using CSR, even though SSR is enabled on the server. To handle this transition effectively, enabling the SSR flag in the admin dashboard ensures that the care search script will load the page from the server to use SSR.

### How to Enable the SSR Flag:
1. Navigate to the Care Search Admin Dashboard.
2. Locate the **SSR Setting** in the settings panel.
3. Toggle SSR **ON**.

Once this flag is activated, the Care Search script will automatically load profile pages using server-rendered content.


## Test and Optimize
Once SSR is implemented and turned on, test your site to ensure that the correct content is being loaded, and that it appears quickly in search engine crawlers.

## FAQs
**Q: Will SSR guarantee better SEO?**

A: SSR can help make your content more accessible to search engines, but SEO depends on various factors like page speed, mobile-friendliness, and overall site quality.

