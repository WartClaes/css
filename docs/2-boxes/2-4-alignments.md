# 2.4 Alignment

In this chapter we'll see how to align text and elements.

## Content

- [Text alignment](#text-alignment)
- [Element alignment](#element-alignment)

---

## Text Alignment

To align text in a certain element we use the `text-align` property.

#### justify

When using `justify`, each line of the text will stretch to the width of the element (except for the last line).

##### start/end

These values make multiple language support easier. When the language is read from left to right `start` will be the
same as `left`, and `end` will be the same as `right`.

When the language is read from right to left `start` will be the same as `right`, and `end` will be the same as `left`.

Too bad the support of [logical properties](http://caniuse.com/#search=logical) isn't that high.

#### Example

```css
.selector {
  text-align: left | center | right | justify | start | end;
}
```

---

## Element Alignment

### Horizontally

To align an element horizontally we use the `margin` property.

#### Align left

An element is by default aligned `left`, but to complete our examples here is an explicit example.

```css
.element {
    margin-right: auto;
    width: 100px;
}
```

#### Align right

```css
.element {
    margin-left: auto;
    width: 100px;
}
```

#### Align Center

```css
.element {
    margin: 0 auto; /* Shorthand notation */
    margin-left: auto; /* Full notation */
    margin-right: auto; /* Full notation */
    width: 100px;
}
```

### Vertically

Well use the HTML markup underneath to create all our examples:

```html
<div class="container">
    <div class="selector">
        I'm vertically Centered
    </div>
</div>
```

#### Positioning and transforming

The first method we'll take a look at is using a relative position and a tranform. Notice that we specify a top of 50%
which refers to 50% of the height of the container, and we translate the element on the y-axis with -50% which refers to
the height of the element itself (because we're using transform).

#### Example

```css
.container {
    height: 500px;
}

.selector {
    position: relative;
    top: 50%;
    transform: translateY(-50%);
}
```

#### Tables to the rescue

We can have a somewhat simular result by using table layouts. In this solution the element will be as high as it's
container but will align the it's content vertically.

#### Example

```css
.container {
    display: table;
    height: 500px;
}

.selector {
    display: table-cell;
    vertical-align: middle;
}
```

#### Flexbox magic

The ultimate solution to aligning is flexbox. Flexbox gives us total control of how we want to align and size our elements.
We'll go deeper into flexbox in a later chapter.

#### Example

```css
.container {
    align-items: center;
    display: flex;
    height: 500px;
}
```
