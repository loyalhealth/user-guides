---
name: Structured Data
---

## HTML Schema Markup | Structured Data

Search engines work hard to understand the content of a page. You can help them by providing explicit clues about the meaning of a page by including structured data on the page. Structured data is a standardized format for providing information about a page and classifying the page content.

Search engines use structured data that it finds on the web to understand the content of the page, as well as to gather information about the web and the world in general. Loyal advises using Microdata as the preferred structured data markup when implementating star ratings and reviews.

### What is Microdata?

Microdata uses a supporting vocabulary to describe an item and name-value pairs to assign values to its properties. Microdata is an attempt to provide a simpler way of annotating HTML elements with machine-readable tags.

For your Providers/Doctors, this data can be represented by the following, and allows engines like Google to display star ratings in their search results:

```html
<!—- This is example HTML of a potential Provider page with Microdata -->

<section itemscope itemtype="http://schema.org/Physician">
  <!—- Ensure your doctor's name has a prop -->
  <h2 class="doctor-title" itemprop="name">Rachel Smith, MD</h2>

  <!—- Make sure to include the image prop -->
  <img itemprop="image" src="https://healthsystem.org/providers/58310.jpg" />

  <p
    itemprop="aggregateRating"
    itemscope
    itemtype="http://schema.org/AggregateRating"
  >
    <span itemprop="ratingValue">4.8</span> out of 5
    <span itemprop="ratingCount">344</span> Ratings, 0 Comments
  </p>
</section>
```

The keys you use for the JSON-LD object will be the same as the `itemProp` that are used when using html markup for structured data.

To read further on JSON-LD check out

- Schema.org's documentation on the [Physician Schema](https://schema.org/Physician)
- [JSON-LD.org's](https://json-ld.org/) documentation and JSON-LD "playground."
