## 5.1 Transitions

Transitions and animations are both a CSS3 specification.

A transition is there to alter the appearance of an element when a state change happens (eg. hover, focus, ...).

## Content

- [Properties](#properties)
- [Duration](#duration)
- [Delay](#delay)
- [Values of different lengths](#values-of-different-lengths)
- [Timing function](#timing-function)
- [Shorthand](#shorthand)

---

## Properties

The default behaviour if `transition-property` is that all properties are affected by the transition. When you define
specific properties, only these will be affected by all the transitions. The properties that aren't defined in this list
will be affected by the state change, but will not follow the other tranition propeties such as delays, ...

When transitioning multiple properties, you can create a comma seperated list. If you don't specify this list or set the
value to `all` you need to take in mind that properties that don't animate now, can animate in the future. So you need
to make sure that you don't break any functionality in your website.

```css
.foo {
    background: hotpink;
    border-radius: 2%;
    transition-property: background, border-radius;
}

.foo:hover {
    background: cyan;
    border-radius: 50%;
}
```

### Transitional properties

Not all properties can be transitioned. Only properties that have an identifiable halfwaypoint. For example a `font-size`
can be transitioned since is has clear changeable values, in this case pixels.

`display` on the other hand can not be transitioned because there are no steps in between for example `block` and `inline-block`.

---

### Duration

The duration of a transition can be defined by `transition-duration` in seconds (`s`) or milliseconds (`ms`). This
value may also be frational eg. `.3s`.

When you have defined multiple properties, you can also set multiple duration properties. Each for one property. The
order is mapped to the order of the `transition-property` list. So the first items will pair up, the second will pair
up and so on.

```css
.foo {
    background: hotpink;
    transition-property: background;
    transition-duration: 1s;
}

.foo:hover {
    background: cyan;
}
```

---

## Delay

Apart from setting a `animation-duration`, you can also set a `animation-delay`. This defines the time that the animation
will be stalled before it starts playing. Values for this property are the same as the `transition-duration` property,
seconds (`s`) and milliseconds (`ms`).

```css
.foo {
    background: hotpink;
    transition-property: background;
    transition-duration: 1s;
    transition-delay: 1s;
}

.foo:hover {
    background: cyan;
}
```

---

## Values of different lengths

If you have the following code:

```css
.bar {
    transition-property: background, border-radius, color, height;
    transition-duration: 2s, 4s;
}
```

The lengths of the `transition-property` and the `transition-duration` don't match. In this case the duration will
follow the same rules as applied to for example `margin` The way CSS sees this is:

```css
.baz {
    transition-property: background, border-radius, color, height;
    transition-duration: 2s, 4s, 2s, 4s;
}
```

---

## Timing function

The `transition-timing-function` property is used to set the speed in which a transition is happening. This property
takes a timing function as a value.

You may specify multiple values, which each apply to the corresponding `transition-property`.

### Types of timing functions

Each timing function keyword translates into a [cubic-bezier curve](http://cubic-bezier.com/). These functions are
mathematical functions that describe an acceleration curve so the speed of an element can change over the duraction of a
transition.

Values are mapped according coordinates over an xy-chart. This results in a value of `x1, y1, y2, y2`. The y-values can
be greater than 1.0 which makes the animation to go further then their original position and this gives a bouncing effect.

```css
.quux {
    ...
    transition-timing-function: cubic-bezier(0.0, 0.0, 1.0, 1.0);
}
```

The above value represents the `linear` keyword. Other available keywords are `ease`, `ease-in`, `ease-in-out` and
`ease-out`. An example of these values can be found on [Codepen](http://codepen.io/WartClaes/full/pjpNVO/)

---

## Shorthand

You don't need to write out all the different properties. The CSS specification also provides a shorthand method.

```css
transition
    transition-delay
    transition-duration
    transition-property
    transition-timing-function
```

