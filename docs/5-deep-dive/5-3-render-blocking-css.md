# 5.3 Render Blocking CSS

We know that our browser needs both our HTML \(DOM\) and our CSS \(CSSOM\) to render our page, but how can we limit our
CSSOM?

## Content

- [What is render blocking?](#what-is-render-blocking)
- [Lazy loading CSS](#lazy-loading-css)
- [Media Queries](#media-queries)

---

## What is render blocking?

So now that we know that our browser needs both our DOM and our CSSOM to render our page, it is obvious to say that CSS
is a render blocking resource. Which basically means that our browser will not display our page until it has loaded the
stylesheets. For this reason it is our job to deliver the CSS to the customer as fast as possible.

---

## Lazy loading CSS

With modern frameworks we see that lazy loading is not only applicable on JS but also on CSS. This is the point were we
have to be very carefull. Lazy loading of CSS may increase your site's performance because your initial CSSOM will be alot
smaller, which means that the browser will have it much easier to apply that CSSOM on your DOM.

But on the other hand, lazy loading CSS means that the CSSOM will updated after the page has been rendered, this will
most likely cause a repaint of your screen and even worse, this could cause a **Flash Of Unstyled Content**. Be aware of
these dangers and always compare the benefits with the downsides.

---

## Media Queries

Another way to limit the size of our CSSOM and decreasing our rendering time is correct usage of media queries.

#### Example

```html
<link href="stylesheet.css" rel="stylesheet"/>
<link href="print.css" media="print" rel="stylesheet"/>
<link href="other.css" media="(min-width: 40em)" rel="stylesheet" >
```

In the example above we see that first line has no media attributes, this implies that the browser should block rendering
until that resource is loaded. On the second and third line we see link tags with a media attribute, these resources
will only be blocking the rendering process if the media query matches.

If the media query does not match, the browser will load the resource, but it will not block the rendering process.
Therefor it is advised to use the media attribute to apply media queries, instead of using them inside your CSS file.

