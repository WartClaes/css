## 4.2 Animations

The difference between the two is that a transition is there to alter the appereance of an element when a state change
happens (eg. hover, focus, ...).

Animations are for changing appearences over time by using keyframes. This way you can chain multiple transitions inside
those different keyframes.

## Content

- [Keyframes](#keyframes)
- [Animation](#animation)

---

## Keyframes

A keyframe is actually a breakpoint within the animation. These can be accessed using the at-rule `@keyframes`.

To use this at-rule we start by defining a name for the animation right after the declaration. This name will be used by
the `animation-name` property to match the animation with the correct keyframe list.

Each `@keyframes` rule has a list of keyframe selectors. Such selector has a percentage and a block containing the styles
of that keyframe. These selectors can be put in any order. The CSS engine will handle them according their percentage.

In order to be a valid list, each `@keyframes` rule should have at least have a 0% selector (or the `from` keyword) and
a 100% selector (or the `to` keyword). If these don't exist, the animation will be ignored by the renderer.

The same goes for invalid style properties. They will also be ignored.

#### Examples

```css
@keyframes foo { /* with keyword */
    from {
        color: hotpink;
    }
    to {
        color: cyan;
    }
}

@keyframes bar { /* only percentages */
    0% {
        color: hotpink;
    }
    50% {
        color: rebeccapurple;
    }
    100% {
        color: cyan;
    }
}

@keyframes baz {
    0%, 100% { /* keyframes with the same values can be combined */
        color: hotpink;
    }
    50% {
        color: cyan;
    }
}
```

---

## Animation

The `animation` property can be used to animate other CSS properties like `color`, `height`, ...

### Name

To link the above created `@keyframes` we need to assing it to an element. This can be accomplished by using the
`animation-name` property.

```css
.foo {
    animation-name: foo;
}
```

### Timing

After declaring an `animation-name` we can set some extra properties it inherits from the transition spec. The first one
is `animation-duration`. This property can be set is seconds (`s`) or milliseconds (`ms`).

```css
.foo {
    animation-name: foo;
    animation-duration: 1s;
}
```

A timing function can be set by using `animation-timing-function`. This sets the speed curve of the animation.

```css
.foo {
    animation-name: foo;
    animation-duration: 1s;
    /*
		possible values:
			linear | ease | ease-in | ease-out | ease-in-out |
			cubic-bezier(n,n,n,n) | initial | inherit
		*/
    animation-timing-function: ease-in-out;
}
```

The last timing property is `animation-delay`. This defines the time between loading the element and the start of the
animation. Same as with `animation-duration` the possible values are seconds or milliseconds.

```css
.foo {
    animation-name: foo;
    animation-duration: 1s;
    animation-timing-function: ease-in-out;
    animation-delay: 5s;
}
```

### Iteration

The default iteration value of an animation is 1. It plays from the start untill the end and then it stops. With
`animation-iteration-count` you can define the number of cycles the animation needs to do before stopping.

You can set a number or use the keyword `infinite` so the animation goes on until the end of time.

```css
.foo {
    animation-name: foo;
    animation-duration: 1s;
    animation-timing-function: ease-in-out;
    animation-delay: 5s;
    animation-iteration-count: infinite;
}
```

### Direction

Apart from setting the itteration count, you can also define the direction the animation has using the
`animation-direction` property. This has 4 different values.

The `normal` value plays the animation as intended. It starts at 0% and goes to 100%. The `reverse` value will do the
opposite, starting from 100% and going to 0%.

`alternate` starts as normal but when the animation iteration is done it, the next iteration will play as reverse and
so on. This way you can make a perfect animation that repeats itself fluently.

The last option is `alternate-reverse`. As the name suggests, this combined the properties `alternate` and `reverse`.
Easy.

```css
.foo {
    animation-name: foo;
    animation-duration: 1s;
    animation-timing-function: ease-in-out;
    animation-delay: 5s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
}
```

### Play state

The play state can set an animation in a `running` state or a `paused` state. When pausing, it will resume from its
current state and not start from the beginning.

```css
.foo {
    animation-name: foo;
    animation-duration: 1s;
    animation-timing-function: ease-in-out;
    animation-delay: 5s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
}

.foo:hover {
    animation-play-state: paused;
}
```

### Fill mode

This property defines if the styling of the element should be done before, after or before and after the animation.

`forwards` means that the element will keep the style defined in the last keyframe. `backwards` is the opposite, so the
styling of the first keyframe will be used.

`both` defines behaviours for both `forwards` and `backwards`

```css
.foo {
    animation-name: foo;
    animation-duration: 1s;
    animation-timing-function: ease-in-out;
    animation-delay: 5s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
    animation-fill-mode: forwards;
}

.foo:hover {
    animation-play-state: paused;
}
```

### Shorthand

Of course there is also a shorthand version of this property:

```css
animation:
    animation-name
    animation-duration
    animation-timing-function
    animation-delay
    animation-iteration-count
    animation-direction
    animation-fill-mode
    animation-play-state
```

