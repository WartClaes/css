# 3.3 Grid

Grid Layout is a proposal originally made by the Microsoft team. It takes a different approach then Flexbox since
Flexbox works on a 1 dimensional system whereas Grid layout is a 2 dimensional system covering both rows and columns.

It is the first system that is made for layouting pages. All previous ways was just using properties to hack a layout,
but it always had a downside eg. no vertical alignment, no equal heights, ...

As is the case with Flexbox, Grid Layout also has properties for both parent and child elements. In general they have
been working on aligning a lot of properties and values between Flexbox and Grid Layout. If there is a difference between
them it is probably an error. This specification is still a Candidate Recommendation so it is still subject to changes.

## Content

- [Support](#support)
- [fr Unit](#fr-unit)
- [Parent element properties](#parent-element-properties)
- [Child element properties](#child-element-properties)

---

## Support

| IE | Edge | Firefox | Chrome | Safari |
| :--- | :--- | :--- | :--- | :--- |
| 💩 | 😺 | 😺 | 😺 | 😺 |

💩 IE supports an older version of the spec, prefixed with `-ms-`.

---

## fr unit

Grid Layout also introduces the `fr` unit. This represents a fraction of the free space in the container.

They are not length or percentage units so they cannot be used in for example `calc()`.

---

## Parent Element Properties

### display

The most important property of all, display. This creates the grid container.

```css
.foo {
    display: grid | inline-grid | subgrid;
}
```

> ⚠️ Subgrid is moved to level 2 of the specification but can be used in Firefox.

### grid-template-columns and grid-template-rows

These properties define the columns and the rows of the grid. The values passed into these properties resemble the size of the track.

```css
.parent {
    grid-template-columns: <track-size> ... | <line-name> <track-size> ...;
    grid-template-rows: <track-size> ... | <line-name> <track-size> ...;
}
```

- `<track-size>` can be a length, percentage or a `fr` unit.
- `<line-name>` is a name you can choose. If you don't provide this, the track names are assigned numerical names.
- `auto`

```css
.parent {
    grid-template-columns: 50% 50px auto;
	/* multiple names are also a possibility */
    grid-template-rows: [foo] 50% [bar] 50px [baz quux] auto;
}
```

You can also use the `repeat()` syntax to handle repeating items.

```css
.parent {
    grid-template-columns: repeat(3, [col-start] 20%) 40%;
    /* results in */
    grid-template-columns: [col-start] 20% [col-start] 20% [col-start] 20% 40%;
}
```

The `fr` unit can be used as the following:

```css
.parent {
    grid-template-columns: 1fr 1fr; /* each column is 50% wide */
    grid-template-rows: 20px 1fr 1fr; /* each row takes up 50% of the available space (100% - 20px) */
}
```

### grid-template-areas

`grid-template-areas` defines a named grid area. If a name is repeated, the area will span over the different columns/rows.
The way you write the value of the property resembles the grid visually.

```css
.parent {
    grid-template-areas:
        "<grid-area-name> | . | none | ..."
        "..."
}
```

- `<grid-area-name>` is a name you can choose yourself.
- `.` resembles an empty area
- `none`

Each row has to contain the same amount of columns. This only gives names to areas, not lines. These will be names
automatically, so an area with the name `foo` will have a starting column line of `foo-start` and an ending column line
of `foo-end`.

This results in double naming of lines. The line between area `foo` and area `bar` will have both `foo-end` and
`bar-start` as their name.

```css
.parent {
    grid-template-areas:
        "logo logo header"
        "nav subnav content"
        "footer footer footer";
    grid-template-columns: 50px 200px 1fr;
    grid-template-rows: 50px 1fr 50px;
}
```

### grid-template

`grid-template` is the shorthand version of `grid-template-columns`, `grid-template-rows` and `grid-template-areas`.

```css
.parent {
    grid-template: none | subgrid | <grid-template-rows> / <grid-template-columns>;
}
```

- `subgrid` sets `grid-template-columns` and `grid-template-rows` to `subgrid`
- `<grid-template-rows> / <grid-template-columns>` sets `grid-template-columns` and `grid-template-rows` to the given values
- `none`

It also works with a more complicate value which also specifies `grid-template-areas`. The following code has the same
result as the previous example.

```css
.parent {
    grid-template:
        "logo logo header" 50px
        "nav subnav content" 1fr
        "footer footer footer" 50px
        / 50px 200px 1fr;
}
```

### grid-column-gap and grid-row-gap

Just like the name already tells you, these properties set the width of the gutters between rows/columns.

```css
.parent {
    grid-column-gap: <line-size>;
    grid-row-gap: <line-size>;
}
```

- `<line-size>` can be any length value.

```css
.parent {
    grid-template-columns: 50px 200px 1fr;
    grid-template-rows: 50px 1fr 50px;
    grid-column-gap: 10px;
    grid-row-gap: 20px;
}
```

### grid-gap

`grid-gap` is the shorthand for `grid-column-gap` and `grid-row-gap`.

```css
.parent {
    grid-gap: <grid-row-gap> <grid-column-gap>;
}
```

If only one value is provided, both `grid-row-gap` and `grid-column-gap` have the same value.

```css
.parent {
    grid-template-columns: 50px 200px 1fr;
    grid-template-rows: 50px 1fr 50px;
    grid-gap: 20px 10px;
}
```

### justify-items

Aligns the content off all grid items along the row-axis. Default value is `stretch`.

```css
.parent {
    justify-items: start | end | center | stretch;
}
```

### align-items

Aligns the content off all grid items along the column-axis. Default value is `stretch`.

```css
.parent {
    align-items: start | end | center | stretch;
}
```

### justify-content

If the width of your grid is smaller then the container it sits in, which can happen if you set all your grid items in
`px`, `justify-content` aligns your grid on the row axis.

Default value is `start`.

```css
.parent {
    justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```

### align-content

If the width of your grid is smaller then the container it sits in, which can happen if you set all your grid items in
`px`, `align-content` aligns your grid on the column axis.

Default value is `start`.

```css
.parent {
    align-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```

### grid-auto-columns and grid-auto-rows

If a grid item is positioned outside the range of columns/rows created by `grid-template-rows` or `grid-template-columns`,
they are stored on implicit grid tracks. `grid-auto-columns` and `grid-auto-rows` specify the size of these implicit tracks.

```css
.parent {
    grid-auto-columns: <track-size> ...;
    grid-auto-rows: <track-size> ...;
}
```

- `<track-size>` can be a length, percentage or fr value

```css
.parent {
    ...
    grid-template-columns: 20px;
    grid-template-rows: : 20px;
    grid-auto-columns: 40px;
    grid-auto-rows: 40px;
    ...
}

.child-1 {
    /*
        This way the child is positioned at col 2/row 2.
        The grid is only 1 col/1 row, so the implicit generated tracks will be 40px wide.
    */
    grid-column: 2;
    grid-row: 2;
}
```

### grid-auto-flow

If you have grid items that aren't explicitly placed in the grid, they are automatically placed. The `grid-auto-flow`
property handles the way they are placed into the grid.

```css
.parent {
    grid-auto-flow: row | column | row dense | column dense;
}
```

- `row` places the grid items to fill each row, adding rows if necessary
- `column` places the grid items to fill each column, adding columns if necessary
- `dense` fills up the holes in the grid if smaller items come up later on. Grid items might appear out of order this way.

### grid

`grid` is a shorthand for all the previous properties.

```css
.parent {
    grid: none | <grid-template-rows> / <grid-template-columns> | <grid-auto-flow> [<grid-auto-rows> [/ <grid-auto-columns>]];
}
```

---

## Child Element Properties

### grid-column-start, grid-column-end, grid-row-start and grid-row-end

These properties define the positioning of the elements by referring to the specific grid lines.

```css
.child {
    grid-column-start: <number> | <name> | span <number> | span <name> | auto;
    grid-column-end: <number> | <name> | span <number> | span <name> | auto;
    grid-row-start: <number> | <name> | span <number> | span <name> | auto;
    grid-row-end: <number> | <name> | span <number> | span <name> | auto;
}
```

* `<line>` can be a number or a name that refers to the named grid line
* `span <number>` the item will span over the given number of grid tracks
* `span <name>` will span the item across the rows/columns until it hits the provided name
* `auto` is default and will place the item automatically

```css
.child {
    grid-column-start: 2;
    grid-column-end: five;
    grid-row-start: row1-start
    grid-row-end: 3
}
```

### grid-column and grid-row

These properties are shothands for their respective `-start` and `-end` siblings.

```css
.child {
    grid-column: <start-line> / <end-line> | <start-line> / span <value>;
    grid-row: <start-line> / <end-line> | <start-line> / span <value>;
}
```

```css
.child {
    grid-column: 3 / span 2;
    grid-row: third-line / 4;
}
```

### grid-area

Assigns a name to a grid item so it can be used in `grid-template-areas`. This property can also be used ad an even
shorter version of `grid-column` and `grid-row`.

```css
.child {
    grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
}
```

```css
.child {
    grid-area: content;
}

/* shorthand version of grid-column and grid-row */
.child {
    grid-area: third-line / 4 / 3 / span 2;
}
```

### justify-self

`justify-self` is much like the grid-containers `justify-items`.

It align the grid item's content along the row axis.

```css
.child {
    justify-self: start | end | center | stretch;
}
```

### align-self

`align-self` is much like the grid-containers `align-items`.

It align the grid item's content along the column axis.

```css
.child {
    align-self: start | end | center | stretch;
}
```

