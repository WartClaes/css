# 2.5 Shadows

Here we find the explanation how to make box-shadows.

## Content

- [Box shadows](#box-shadows)

---

## Box shadows

The `box-shadow` property allows you to set one or more box-shadows on an element. It is widely supported and even if it
is not supported, the fact that a shadow is not shown should not break your design.

The value exists of 2, 3 or 4 `length` values, an optional `color` value and an optional `inset` keyword.

#### Example

```css
.foo {
    box-shadow: 5px 5px 5px rgba(0, 0, 0, .2);
}
```

- The first of the length values is the **horizontal offset** (distance to the right). If negative, the distance is to the left.
- The second of the length values is the **vertical offset** (distance to the bottom). If negative, the distance is to the top.
- The third value (optional) is the **blur radius**. The bigger the value, the bigger the blur. If not provided, the value is `0`.
- The fourth and final lenght value is the **spread**. Positive values will cause the shadow to expand and grow bigger,
negative values will cause the shadow to shrink. If not provided, the value is `0`.
- The **inset** keyword changes the shadow to one inside the frame.
- The **color** determines the actual color of the shadow. If not set, it depends on the browser what color is sets.

#### Example

```css
.foo {
    box-shadow: inset 5px 5px 5px 5px rgba(0, 0, 0, .2);
}
```

It is possible to define multiple shadows on a single element. The different shadows should be comma seperated.

#### Example

```css
.foo {
    box-shadow:
        -5px -5px 5px rgba(0, 0, 0, .2),
        5px 5px 5px rgba(0, 0, 0, .2);
}
```
