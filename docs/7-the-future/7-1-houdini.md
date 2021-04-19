## 7.1 Houdini

The biggest complain with CSS? I have this awesome new thing called _favorite CSS thing here_ but I can't use it because
of browser support. Take Grid Layout for example. The initial idea for the specification dates from november 2012.

The actual implementation in browser only came in may 2017. And that is only for the new ones. Everybody still needs to
support some sort of older browser.

But wait, there is good news! The future is bright for CSS with the new W3C task force called **Houdini** 🎩.

## Houdini you say?

Yes, Houdini. Their main focus is explaining the magic of styling and layout in a browser. The way they want to reach
that goal is by creating a series of API's that give developers the power of browser. With these API's you can extend
CSS itself and hook it into the browsers magic.

By providing these API's you can write your own polyfills or plugins that gives you that shiny new feature you always
wanted. And although it won't be easy, it will definitely not take 5 years to finish it.

## The magic

How can we access the _Tools of the Gods_? The answer is quite simple. JavaScript. It already has the power to reach
some parts of the CSSOM, so why not make the rest of the rendering pipeline available as well.

But I can write CSS polyfills in JavaScript already? Yes that is correct. But doing that you still can't access the way
the browser actually renders the pixels. For example you can create a script that sets the same height on all the
elements. But what you actually do is waiting until the browser completes it's work, take the biggest height and
re-apply it to the other elements, thus restarting the rendering pipeline.

It does not seem that this is a big problem. But performance wise it is a hell to maintain this. You never know exactly
how much your polyfill needs to be executed on for example scroll events, keyboard events, ... In the end it will all
feel slow and not at all user friendly.

## But should we do this?

That is a thing a lot of people ask themselves. Should I really go through learning this whole new technology so in the
end I can do what I've been doing for years, creating simple websites? The answer is yes, you should do it. It is not
only you who can benefit from this, but everyone who creates websites can use your features.

And as an additional upside,the web gets a lot more normalized. Which is eventually what we want. Developers have been
doing the same with projects like jQuery, Angular and so many more other frameworks. They all normalize the way of
working so it is easier for
everyone.

Imagine using new features as `position: sticky;` in a way that it is natively build, performant and cross-platform.
Reaching this goal is the purpose of the Houdini Task Force.

## What are they working on?

The specification contains 8 \(at the moment\) API's. Some of them are just ideas, others are more concrete.

### Custom Properties

This is one of the best known features of Houdini. But most people know it because of the name `css variables`.
Although this is a bigger implementation then just the variables, the idea stays the same.

Custom properties adds types to properties. This means that because we know what the type of a property is, we can
animate and transition it. Something that is not possible with the css variables implementation.

```javascript
CSS.registerProperty({
	name: "--my-color",
	syntax: "<color>",
	initialValue: "black"
});
```

```css
.theme--red {
    --my-color: red;
    background-color: var(--my-color);
    transition: background-color 1s ease-in;
}

.theme--green {
    --my-color: green;
}
```

### CSS Typed OM

An other big change will be the typed OM. You can see it as CSSOM version 2.

The way the current CSSOM works is completely string based. A pixel value is a string, a color is a string, ...
During the parsing step, the browsers tries to understand the intended value. By creating a CSSOM where the typing is
linked to the value, the browser can skip this step and become more performant in building the actual render tree.

### CSS Layout API

The CSS layout API allows developers to create their own layout module. E.g. values that can be passed into `display`.
This way you can have the same performance as for example `display: grid;`. A great example would be `display: masonry`.

```javascript
registerLayout('masonry', class {
    static get inputProperties() {
        return ['width', 'height']
    }

    static get childrenInputProperties() {
        return ['x', 'y', 'position']
    }

    layout(children, constraintSpace, styleMap, breakToken) {
        // Layout logic goes here.
    }
}
```

The code above would be applied as such:

```css
body {
    display: layout('masonry');
}
```

### CSS Paint API

CSS Paint API is similar to the CSS Layout API. It allows developers to create Paint modules. The API can be implemented
in properties where an image can be passed such as `background-color`.

It would look something like this:

```javascript
registerPaint('circle', class {
    static get inputProperties() { return ['--circle-color']; }
    paint(ctx, geom, properties) {
        // Change the fill color.
        const color = properties.get('--circle-color');
        ctx.fillStyle = color;
        // Determine the center point and radius.
        const x = geom.width / 2;
        const y = geom.height / 2;
        const radius = Math.min(x, y);
        // Draw the circle \o/
        ctx.beginPath();
        ctx.arc(x, y, radius, 0, 2 * Math.PI, false);
        ctx.fill();
    }
});
```

To use it on the element, the following syntax is used:

```css
.bubble {
    --circle-color: blue;
    background-image: paint('circle');
}
```

### Worklets

Worklets are similar to webworkers. They are entry points to include scripts in the rendering pipeline. They allow the
extension of the rendering engine while keeping guarantees which rendering engine rely on.

