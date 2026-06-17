# Tending the Webpage: CSS + JS Cheatsheet!

---

## HTML - creating content inside your plot

```HTML
<div></div>       <!-- a generic box / container -->
<p></p>           <!-- a paragraph of text -->
<span></span>     <!-- a small inline bit of text -->
<img src="">      <!-- an image (no closing tag) -->
<a href=""></a>   <!-- a link -->
<h1></h1>         <!-- a big heading (h2, h3 … get smaller) -->
<ul></ul>         <!-- a bulleted list -->
<li></li>         <!-- one item inside a list -->
```

*Class and id* go on the opening tag so CSS and JS can find and style them. *Class* is reusable and many elements can share it (.flower). *Id* names one specific element (#poem).

```HTML
<div class="plot" id="plot-001"></div>
<img class="seedling" src="sprout.png">
<p class="note">something growing here</p>
```

### Nesting

Make sure your opening + closing tags match and that things are **nesting** properly inside each other, like boxes inside boxes.

Only close a tag once everything inside is also closed. Read this from the outside in: *a garden contains a plot which contains a thought above a flower*.

```HTML
<div class="garden">
  <div class="plot">
    <p>a thought</p>
    <img src="flower.png">
  </div>
</div>
```

**Good rules of thumb:**
- Write your opening and closing tags first, *then* put everything inside.
- Don't cross tags like this:
```HTML
<div><p></div></p>
```
- Remember, some tags don't have closing ones like *img* and *br*.

---

## CSS — what your class actually *looks* like

This is where you define what a class means visually so you can add it with JS.

### Class vs ID

```css
.class-name { /* resuable, MANY elements can share. any styles here will affect ALL instances with the same name */

}

#id-name { /* names ONE specific element, e.g. #plot-1 */ 

}
```

### Basic appearance

```css
.watered { /* you can name this anything that makes sense */
  color: #2a6f4f;
  background-color: #eaf6ee;
  opacity: 1;
}
```

### Size and shape

```css
.grown {
  transform: scale(1.3);   /* bigger */
  width: 200px;             /* size */
  border-radius: 50%;      /* rounded corners */
}
```

### Motion and transition

Without this, changes snap instantly. With it, they ease in:

```css
.plot {
  transition: all 0.6s ease;
}
```

### Animation (for ongoing or looping effects)

Check out [W3schools](https://www.w3schools.com/css/css3_animations.asp) for more detailed explanations of animations.

```css
.perennial {
  animation: sway 3s ease-in-out infinite;
}

@keyframes sway {
  0%   { transform: rotate(0deg); }
  50%  { transform: rotate(5deg); }
  100% { transform: rotate(0deg); }
}
```

### Hover-only effects

```css
.tool:hover {
  cursor: grab;
  transform: scale(1.1);
}
```

---

## JavaScript — making your tool *do* something 

### Finding elements

Every JS action follows the same shape:

```javascript
element.action("something")
```

- **element**: what you're acting on (e.g. 'plot', or something inside it like 'flower')
- **action**: what you're doing (changing color, adding text, etc.)
- **something**: the value (class name, text string, color hex code, etc.)

**Class vs ID in JS:**
- In querySelector, use a **dot** for class and **hash** for id: ".flower" vs "#poem"
- In classList.add / remove / toggle, use the name *without the dot*.

You can choose the scope for what you want to act on:

```javascript
// your plot
plot.classList.add("watered")

// one thing inside your plot
plot.querySelector("#poem").textContent = "hello"

// all of something inside your plot
plot.querySelectorAll(".flower").forEach(el => el.classList.add("blooming"))

// all of something on the whole page
document.querySelectorAll(".flower").forEach(el => el.classList.add("blooming"))
```

### The core mechanism: classes

The **simplest thing** for your tool to do is to add, remove, or toggle a *class* on an element. That class contains the CSS styling.

```javascript
// doing something to the whole plot
plot.classList.add("watered")     // add a class
plot.classList.remove("dormant")  // remove a class
plot.classList.toggle("blooming") // on if off, off if on

//doing something to an element inside the plot
plot.querySelectorAll(".flower").forEach(el =>
      el.classList.add("watered"))
```

If your tool changes how something *looks* or *behaves*, this is probably the only JS you need; you would define the look/behavior *in CSS*.

### Creating + Adding

You can use your tool to add something new to the plot via HTML:

```javascript
// add another flower (text)
plot.innerHTML += '<div class="flower">🌸</div>'

// add another flower (image)
plot.innerHTML += '<div class="flower"><img src="flower.png"></div>'
```

*Note: += keeps what's already in there and adds more, whereas = just replaces*

### Changing content

If your tool changes elements (e.g. words) inside the plot:

```javascript
const poem = plot.querySelector("#poem") // selecting the text element first
poem.textContent = "a new thought"     // changes the text
poem.innerHTML = "<em>a new thought</em>"  // allows HTML tags inside
```
*Note about variables: we defined a const variable above. You could also do it this way:*

```javascript
plot.querySelector("#poem").textContent = "a new thought"
```

### Direct style changes

Usually CSS classes are cleaner, but sometimes you want to set one specific style directly:

```javascript
// whole plot
plot.style.opacity = "0.5"
plot.style.transform = "scale(1.2)"
plot.style.fontSize = "12px"
plot.style.color = "#ff00ff"

// an element inside the plot
plot.querySelector(".image").style.opacity = "0.5"
```
*Do you see what's being replaced here?*

### Changing attributes

Useful for swapping an image, or changing a link:

```javascript
plot.querySelector(".image").setAttribute("src", "new-image.png")
plot.querySelector("#link").setAttribute("href", "https://example.com")
```

---

## Stuck? Troubleshoot in this order:

1. Open the browser console (right-click → Inspect → Console tab) and look for red errors
2. Check that your class name matches exactly in both the JS and the CSS — typos are the #1 culprit
3. Check that the element you're targeting actually exists in the HTML
4. Ask a neighbor
5. Ask Nicci
