# 6.2 Preprocessors

In this chapter we'll take a closer look at some tools that make CSS development a lot easier.

## Content

- [Available Preprocessors](#available-preprocessors)
- [Compiling](#compiling)
- [Sass](#sass)

---

## Available Preprocessors

The frontend world is evolving quickly and in a few years, many have taken a shot to create the perfect preprocessor for
CSS. Here is a small overview of the available preprocessors.

- [Sass](http://sass-lang.com/)
- [Less](http://lesscss.org/)
- [Stylus](http://learnboost.github.io/stylus/)
- [Compass](http://compass-style.org/)
- ...

While each of them has their pro's and con's, you'll mostly end up in a project using Sass (or compass, which is
basically the same as sass on drugs). We'll now take a closer look at some of the features of Sass.

---

## Compiling

Now that we are using a preprocessor we'll need to compile our source files into css. There are several tools to do this
(such as grunt, gulp, webpack, ...) and most modern IDE's have a compiler built in.

- [gulp-sass](https://www.npmjs.com/package/gulp-sass)
- [sass-loader](https://github.com/jtangelder/sass-loader)
- [grunt-sass](https://github.com/sindresorhus/grunt-sass)

---

## Sass

Sass has two syntaxes, `.sass` files which use the old syntax, and `.scss` which use the new syntax. Let's just forget
about the `.sass` syntax for now, `.scss` syntax is better for reasons..

### Variables

The first feature you'll find yourself using a lot, are variables. Variables are one of the biggest missing features in CSS.

**Sass**

```scss
$my-favorite-color: #f00;

.example {
    color: $my-favorite-color;
}
```

**CSS**

```scss
.example {
    color: #f00;
}
```

### Looping

Thanks to Sass we're able to loop and dynamically generate some css.

**Sass**

```scss
@for $i from 1 through 3 {
    .item-#{$i}{
      width: 100px * $i;
    }
}
```

**CSS**

```css
.item-1 {
    width: 100px;
}

.item-2 {
    width: 200px;
}

.item-3 {
    width: 300px;
}
```

In the example above you see that we have two ways to use variables. When using a variable as value or part of the value,
we can use the variable without anything more. When using a variable as part of the CSS syntax (inside the selector,
property, or as unit) we must use the `#{$variable}` syntax.

### Mixins

Sass allows us to create a reusable part of css. These are called mixins and we're able to include mixins wherever we
need them.

**Sass**

```scss
@mixin link {
    color: hotpink;
    text-decoration: underline;
}

a {
    @include link;
}

button {
    @include link;
    border: solid thin hotpink;
    padding: 10px;
    margin: 10px;
}
```

**CSS**

```css
a {
    color: hotpink;
    text-decoration: underline;
}

button {
    color: hotpink;
    text-decoration: underline;
    border: solid thin hotpink;
    padding: 10px;
    margin: 10px;
}
```

We're also able to add parameters to our mixin as following.

**Sass**

```scss
@mixin link($color: hotpink) {
    color: $color;
    text-decoration: underline;
}

a {
    @include link;
}

button {
    @include link(rebeccapurple);
    border: solid thin rebeccapurple;
    padding: 10px;
    margin: 10px;
}
```

**CSS**

```css
a {
    color: hotpink;
    text-decoration: underline;
}

button {
    color: rebeccapurple;
    text-decoration: underline;
    border: solid thin rebeccapurple;
    padding: 10px;
    margin: 10px;
}
```

### Extend

In some cases we write duplicate code in CSS or we're forced to add multiple classes on an HTML element just to achieve
a certain goal. A small example will make this clear.

**Option 1: repeat CSS**

**HTML**

```html
<button class="btn-primary">Example</button>
```

**CSS**

```css
.btn {
    background-color: hotpink;
    border: solid thin;
    padding: 10px;
}

.btn-primary {
    background-color: rebeccapurple;
    border: solid thin;
    padding: 10px;
}
```

**Option 2: clutter HTML**

**HTML**

```html
<button class="btn btn-primary">Example</button>
```

**CSS**

```css
.btn {
    background-color: hotpink;
    border: solid thin;
    padding: 10px;
}

.btn-primary {
    background-color: rebeccapurple;
}
```

**Option 3: do it the Sass way**

**HTML**

```html
<button class="btn-primary">Example</button>
```

**SCSS**

```scss
.btn {
    background-color: hotpink;
    border: solid thin;
    padding: 10px;
}

.btn-primary {
    @extend .btn;
    background-color: rebeccapurple;
}
```

**CSS**

```css
.btn,
.btn-primary {
    background-color: hotpink;
    border: solid thin;
    padding: 10px;
}

.btn-primary {
    background-color: rebeccapurple;
}
```

**Option 4: placeholder selectors**

Sometimes we want to achieve the same result as option 3, but without making the `.btn` class available for usage.
We can achieve this by creating placeholder selectors.

**SCSS**

```scss
%btn {
    border: solid thin;
    padding: 10px;
}

.btn-primary {
    @extend %btn;
    background-color: rebeccapurple;
}

.btn-secondary {
    @extend %btn;
    background-color: hotpink;
}
```

**CSS**

```css
.btn-primary,
.btn-secondary {
    border: solid thin;
    padding: 10px;
}

.btn-primary {
    background-color: rebeccapurple;
}

.btn-secondary {
    background-color: hotpink;
}
```
