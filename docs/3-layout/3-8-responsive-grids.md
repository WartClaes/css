# 3.8 Responsive Grids

Now that we know how to write media queries and how to create our favorite grid system, we're able to create a responsive grid.

We'll use flexbox to create our grid system. Flexbox has some reasonable defaults so it's not that much work to create a grid system.

## Content

- [Grid](#grid)
- [Cells](#cells)
- [Offset](#offset)
- [Responsiveness](#responsiveness)
- [SCSS](#scss)

---

## Grid

The first thing we'll need to do is create a container element for our grid system.

```css
.grid {
	display: flex;
	flex-wrap: wrap;
}
```

- `display: flex` makes our grid behave as a flexbox container.
- `flex-wrap: wrap` makes our items wrap to multiple lines when overflowing.

---

## Cells

After that we've create a grid, we can now create the different cells for our grid. We'll follow the mobile first
approach so our 'default' cells will have the small suffix.

```css
.cell {
	box-sizing: border-box;
	padding: 5px;
}
```

- `box-sizing: border-box` makes our padding and border part of the width. Therefor we don't have to take padding our
borders into account when setting the width of the elements.
- `padding: 5px` adds a 10px gutter between different cells \(5px on each side of the cell\).

```css
.cell-s-1 {
	flex-basis: 8.33%;
}

.cell-s-2 {
	flex-basis: 16.66%;
}

...
```

- `flex-basis: 8.33%` sets the width of our cell, before distributing the remaining width.

---

## Offset

In some cases we want to add some extra margin to our cells. This can be done by adding some margin to the cells, it is
really handy if a grid comes with some default classes for these offsets.

```css
.offset-s-1 {
	margin-left: 8.33%;
}

.offset-s-2 {
	margin-left: 16.66%;
}

...
```

- `margin-left: 8.33%` adds left margin to the cell.

---

## Responsiveness

After that we have set up our basic grid system, we can add some responsiveness. Responsiveness on a grid system is no
more then, when a certain breakpoint is met, providing some extra classes. We'll trust on the cascading part of CSS to
apply the correct width to our element.

```css
.cell-s-1 {
	flex-basis: 8.33%;
}

.cell-s-2 {
	flex-basis: 16.66%;
}

.offset-s-1 {
	margin-left: 8.33%;
}

.offset-s-2 {
	margin-left: 16.66%;
}

@media (min-width: 768px) {
	.cell-m-1 {
		flex-basis: 8.33%;
	}

	.cell-m-2 {
		flex-basis: 16.66%;
	}

	.offset-m-1 {
		margin-left: 8.33%;
	}

	.offset-m-2 {
		margin-left: 16.66%;
	}
}

@media (min-width: 1024px) {
	.cell-l-1 {
		flex-basis: 8.33%;
	}

	.cell-l-2 {
		flex-basis: 16.66%;
	}

	.offset-l-1 {
		margin-left: 8.33%;
	}

	.offset-l-2 {
		margin-left: 16.66%;
	}
}

...
```

---

## SCSS

Sass (.scss) will make it so much easier to create a grid system, since we can loop and calculate thing at compile time. We created the grid above with sass.

#### Example

```scss
$cells: 12;
$gutter: 10px;
$breakpoints: (
	's': 'default',
	'm': '(min-width: 768px)',
	'l': '(min-width: 1024px)'
);

.grid {
	display: flex;
	flex-wrap: wrap;
}

.cell {
	box-sizing: border-box;
	padding: $gutter / 2;
}

@mixin grid($breakpoint-name) {
	@for $i from 1 through $cells {
		$size: 100%/$cells*$i;

		.cell-#{$breakpoint-name}-#{$i}{
			flex-basis: $size;
		}

		.offset-#{$breakpoint-name}-#{$i}{
			margin-left: $size;
		}
	}
}

@each $breakpoint-name, $breakpoint in $breakpoints {
	@if $breakpoint == default {
		@include grid($breakpoint-name);
	} @else {
		@media #{$breakpoint} {
			@include grid($breakpoint-name);
		}
	}
}
```
