# 6.1 Project Structure

When starting a new project one of the first things that must be done is finding out how you want to organize your files.
Many best practises have shown up and each one of them has its benefits.

We added this topic to this course because we find that in many projects the chosen approach is strictly followed for our
script and view files. But when it comes to CSS we tend to be less strict about it. We'll create a `style.css` file and
start writing our base CSS code in there.

**style.css**

```css
body {
    font-family: Arial;
}

h1 {
    font-size: 30px;
}

h2 {
    font-size: 24px;
}
```

Afterwards we'll start adding features to the same file.

**style.css**

```css
body {
    font-family: Arial;
}

h1 {
    font-size: 30px;
}

h2 {
    font-size: 24px;
}

.btn {
    background-color: hotpink;
    border-radius: 3px;
    color: white;
    padding: 10px;
}

.navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: 50px;
    background-color: #f00;
}
```

A while later we notice that one of our feature, the button, needs some extra code so we'll just add it to the stylesheet.

**style.css**

```css
body {
    font-family: Arial;
}

h1 {
    font-size: 30px;
}

h2 {
    font-size: 24px;
}

.btn {
    background-color: hotpink;
    border-radius: 3px;
    color: white;
    padding: 10px;
}

.navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: 50px;
    background-color: #f00;
}

.btn-primary {
    background-color: rebeccapurple;
}
```

We see that our stylesheet already start to be unreadable and we've only added some basic styling and added a button and
a navbar. What if we try to follow the feature based approach just as strict for our CSS files as for our other files.

```
- src
    - components
      - button
          - button.html
          - button.css
      - navbar
          - navbar.html
          - navbar.css
    - app
      - featureA
          - featureA.html
          - featureA.css
          - featureA.js
    - common
      - common.css
```

**common.css**

```css
body {
	font-family: Arial;
}

h1 {
	font-size: 30px;
}

h2 {
	font-size: 24px;
}
```

**button.css**

```css
.btn {
	background-color: hotpink;
	border-radius: 3px;
	color: white;
	padding: 10px;
}

.btn-primary {
	background-color: rebeccapurple;
}
```

**navbar.css**

```css
.navbar {
	position: fixed;
	top: 0;
	left: 0;
	right: 0;
	height: 50px;
	background-color: #f00;
}
```

### Conclusion

Though this chapter has a strong personal interpretation, we advise to treath your CSS files the same way as you treath
your script/view files. They contain as much business logic as the rest of your source files and they deserve to be
treated equally!

