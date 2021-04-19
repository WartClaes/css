# 6.3 BEM

BEM is a fronted methodology meaning _Block_, _Element_ and _Modifier_. It is a way of giving clearer names to CSS
classes to improve clarity and readability for other developers.

## Block

A block represents the higher level of a component.

```css
/* eg. .navigation */
.block {
  ...
}
```

---

## Element

An element is a descendent of a block that performs a specific function.

```css
/* eg. .navigation-item */
.block__element {
  ...
}
```

---

## Modifier

The modifier represents a different state of a block or an element.

```css
/* eg. .navigation__item--active */
.block__element--modifier {
  ...
}
```

This way of writing your CSS tells more to a developer just by looking at the selector It is a simplified version of the
HTML structure. By doing this you also create the ability of moving the block around on the page. You won't be limited
to, for example, a position in the header, you can easily put it in the footer

You can also take it all apart and type the following code:

```css
.navigation { ... }
.item { ... }
.active { ... }
```

Here it isn't clear what everything means. `.item` can be an item for everything on the page, the same goes for `.active`.

Of course you can make this better and write this:

```css
.navigation { ... }
.navigation .item { ... }
.navigation .item.active { ... }
```

The problem with this code is that it makes the CSSOM heavier. If we do this on a large scale application, we could get
performance issues when rendering the CSS.

## What if...

... I don't have a block with an element and maybe a modifier, but a simple styling class like `.caps`?

You don't need to make everything BEM. There will always be selectors that doesn't belong a BEM category. Then it will
just be a standalone selector.

Just make sure that you don't exaggerate when applying this methodology. Use it only when necessary which is the hardest
part of BEM.

## The rest

Apart from a CSS naming convention, BEM also provides a file system organization.

They work component based with the same elements used in the CSS selectors. It would look something like this:

```text
blocks/
  navigation/
    item.css
    item_active.css
    item.js
```

