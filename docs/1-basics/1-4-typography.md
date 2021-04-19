# 1.4 Typography

In CSS there are a large amount of value types. Ranging from numerical values to functions. Some are more common then others, but we will take a look at all of them here.

## Content

* [Basics](1-4-typography.md#basics)
* [Custom fonts](1-4-typography.md#custom-fonts)

---

## Basics

Fonts come in different sizes and weights, which makes that there are a lot of properties concerning fonts. But how can you benefit the most from such font in CSS?

### Font-family

It all starts with a `font-family`. This property declares which font you are going to use. The property accepts multiple, comma seperated, values.

The first font is the primary font. If this isn't available, the next font is going to be used and so on.

If you declare a font with a space in it, such as `Comic Sans MS`, the value should be wrapped in quotarion marks `"Comic Sans MS"`.

#### Example

```css
.button {
    font-family: Helvetica, Arial;
}
```

### Font-size

The second one is font-size. The property says it all, it sets the size of the font.

#### Example

```css
.button {
    ...
    font-size: 14px;
}
```

### Font-style

If you want to change the font to italic, you can set is by using `font-style`. The available options are `normal`, `italic`, `oblique` and `inherit`.

#### Example

```css
.button {
    ...
    font-style: italic;
}
```

### Font-weight

The `font-weight` property sets the weight of a font. Shorthands avaiblable are `normal`, `bold`, `bolder`, `lighter` and `inherit`.

#### Example

```css
.button {
    ...
    font-weight: bold;
}
```

Apart from the shorthands, you can set the value ranging from `100` through `900`, with steps of a 100, where `100` is lightest and `900` is the heaviest. For example `bold` equals `700` and `normal` equals `400`.

The fact that you can use the numeric values depend of the font you are using. Not all fonts provide all weights.

#### Example

```css
.button {
    ...
    font-weight: 700;
}
```

### Line-height

`Line-height` is the distance between 2 lines of text. it accepts all the different length values. Most browsers set a default `line-height` of `1.2` \(multiplying factor\).

This property is sometimes used to center text vertically by setting the line-height the same as the height of the block.

#### Example

```css
.button {
    ...
    line-height: 30px;
    height: 30px;
}
```

### Text-decoration

`text-decoration` allows you to add some extra styling to your text. For example it makes it possible to underline your text. By default no text-decoration is added to elements except for specific elements \(like an `<a>` tag\).

#### Example

```css
.button {
    ...
    text-decoration: none | underline | overline | line-through | initial | inherit;
}
```

### Other

* `font-variant`: The font-variant property specifies whether or not a text should be displayed in a small-caps font.
* `letter-spacing`: The letter-spacing property increases or decreases the space between characters in a text.
* `text-transform`: The text-transform property controls the capitalization of text.

### Result

All of these properties combined result in something like this:

#### Example

```css
.button {
    font-family: Helvetica, Arial;
    line-height: 30px;
    font-size: 14px;
    font-style: italic;
    font-weight: bold;

    /* And some eye candy */
    background: #f00;
    display: inline-block;
    height: 30px;
    padding: 20px;
}
```

```markup
<span class="button">
    Button
</span>
```

---

## Custom fonts

Apart from the fonts provided by the system, you can also embed your own font. This can be accomplished by the `@font-face` at-rule.

#### Example

```css
@font-face {
    src: url('fonts/mycustomfont.woff.');
    font-family: 'MyCustomFont';
    font-weight: normal;
    font-style: normal;
}
```

Thanks to this property, developers are not limited to the system fonts available on the device of the user.

Apart from fonts as we know it, you can also use this technique as another solution to embedding icons in a website. Mapping one icon to one unicode character makes it possible to "type" icons and therefore placing them into your HTML.

