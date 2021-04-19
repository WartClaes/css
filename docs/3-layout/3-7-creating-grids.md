# 3.7 Creating grids

In this part we'll take a closer look at different grid systems. To keep the code somewhat readable we'll create a 4
column grid in each example.

## Content

- [Markup](#markup)
- [Table Grid](#table-grid)
- [Floating Grid](#floating-grid)
- [Flexbox Grid](#flexbox-grid)

---

## Markup

We'll use the following markup for each grid.

```html
<div class="row">
	<div class="column column-1">
		.column-1
	</div>
	<div class="column column-3">
		.column-3
	</div>
</div>
<div class="row">
	<div class="column column-2">
		.column-2
		<br />
		<br />
		<br />
		<br />
	</div>
	<div class="column column-2">
		.column-2
	</div>
</div>
<div class="row">
	<div class="column column-4">
		.column-4
	</div>
</div>
```

```css
.row {
	background-color: rebeccapurple;
}

.column {
	background-color: hotpink;
	padding: 20px;
}
```

---

## Table Grid

### pros

- Vertical alignment
- Equal height

### cons

- Hard to make responsive
- Relative margin between columns

#### Example

```css
.row {
	border-spacing: 20px;
	display: table;
	table-layout: fixed;
	width: 100%;
}

.column {
	display: table-cell;
}

.column-1 {
	width: 25%;
}

.column-2 {
	width: 50%;
}

.column-3 {
	width: 75%;
}

.column-4 {
	width: 100%;
}
```

---

## Floating Grid

### pros

- Responsiveness is easier

### cons

- No equal height
- No vertical alignment
- Absolute margin between columns

#### Example

```css
.row {
	display: inline-block;
	width: 100%;
}

.column {
	box-sizing: border-box;
	float: left;
}

.column-1 {
	margin: 1%;
	width: 23%;
}

.column-2 {
	margin: 1%;
	width: 48%;
}

.column-3 {
	margin: 1%;
	width: 73%;
}

.column-4 {
	margin: 1%;
	width: 98%;
}
```

---

## Flexbox Grid

### pros

- Equal height
- Vertical alignment
- Repsonsiveness

### cons

- Browser support

#### Example

```css
.row {
	display: flex;
}

.column-1 {
	margin: 1%;
	width: 23%;
}

.column-2 {
	margin: 1%;
	width: 48%;
}

.column-3 {
	margin: 1%;
	width: 73%;
}

.column-4 {
	margin: 1%;
	width: 98%;
}
```

