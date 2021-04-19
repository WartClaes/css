## 3.6 Media Queries

In this chapter we'll find out what we can achieve with media queries.

## Content

- [Queries](4.1-media-queries.md#queries)
- [@media](4.1-media-queries.md#media)
- [Media Attribute](4.1-media-queries.md#media-attribute)
- [Responsive vs Adaptive](4.1-media-queries.md#responsive-vs-adaptive)

---

## Queries

A media query consist out of a media type and a media feature, different queries can be combined into a more complex query.

### Media Types

- all: all different media types
- screen: only when displayed on a screen
- print: only when in print mode
- speech: only when displayed via screen reader mode

### Media Features

#### height [min-/max-/device-]

The height media feature describes the height of the output device's rendering surface (such as the height of the
viewport or of the page box on a printer).

#### width [min-/max-/device-]

The width media feature describes the width of the rendering surface of the output device (such as the width of the
document window, or the width of the page box on a printer).

#### orientation

Indicates whether the viewport is in landscape (the display is wider than it is tall) or portrait (the display is taller
than it is wide) mode.

#### aspect-ratio [min-/max-/device-]

Describes the aspect ratio of the targeted display area of the output device. This value consists of two positive
integers separated by a slash ("/") character. This represents the ratio of horizontal pixels (first term) to vertical
pixels (second term).

#### color [min-/max-]

Indicates the number of bits per color component of the output device. If the device is not a color device, this value
is zero.

#### color-index [min-/max-]

Indicates the number of entries in the color look-up table for the output device.

#### grid

Determines whether the output device is a grid device or a bitmap device. If the device is grid-based (such as a TTY
terminal or a phone display with only one font), the value is 1. Otherwise it is zero.

#### monochrome [min-/max-]

Indicates the number of bits per pixel on a monochrome (greyscale) device. If the device isn't monochrome, the device's
value is 0.

#### resolution [min-/max-]

Indicates the resolution (pixel density) of the output device. The resolution may be specified in either dots per inch
(dpi) or dots per centimeter (dpcm).

#### scan

Describes the scanning process of television output devices.


### Building logic

We can combine the different types and queries to create complex media queries.

**and**

'and' expression are separated by the 'and' keyword.

```text
screen and (min-width: 760px) and (max-width: 960px)
```

**or**

'or' expression should be written comma separated.

```text
screen and (max-width: 760px), print
```

---

## @media

If we want to use these media queries in our CSS files we can use the @media syntax. This allows us to create a block of
CSS that is only applicable when the query matches your device.

#### Example

```css
.example {
	background-color: hotpink;
}

@media screen and (min-width: 760px) {
	.example {
		background-color: #f00;
	}
}
```

---

## Media Attribute

Though the previous example is functioning correctly, we might end up with large render blocking CSS files (remember the
chapter on render blocking css?). We can avoid this by seperating our css into different files as following. We strongly
advise to use the media attribute, not only is it more performant but your code will be a lot more readable and maintainable.

#### Example

**style.css**

```css
.example {
	background-color: hotpink;
}
```

**style-small.css**

```css
.example {
	background-color: #f00;
}
```

**index.html**

```html
<html>
	<head>
		<link rel="stylesheet" href="style.css"/>
		<link rel="stylesheet" href="style-small.css" media="screen and (max-width: 760px)"/>
	</head>
	<body>
		<div class="example">Resize me please!</div>
	</body>
</html>
```

---

## Responsive vs Adaptive

While media queries help us to work on responsiveness it is important to know the difference between 'responsive' and 'adaptive'. While many websites claim to be responsive, they actually end up adaptive. An example will clear out the difference.

### Adaptive

In adaptive design we use our breakpoints to create new **fixed** layouts.

**Example**

```css
.example {
	margin: 0 auto;
	width: 1400px;
}

@media (max-width: 1000px) {
	.example {
		width: 960px;
	}
}

@media (max-width: 800px) {
	.example {
		width: 760px;
	}
}
```

### Responsive

In responsive design we use our breakpoints to create new **fluid** designs.

**Example**

```css
.example {
  width: 80%;
  margin: 0 auto;
}

@media (max-width: 1000px) {
  .example {
    width: 90%;
  }
}

@media (max-width: 800px) {
  .example {
    width: 95%;
  }
}
```

