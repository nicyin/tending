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

*Class and id* go on the opening tag so CSS and JS can find and style them:

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
.class-name { /* resuable, MANY elements can share e.g. .watered */ 

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

### Filters (good for decay, weather, atmosphere)

Here's a list of other [filters](https://www.w3schools.com/css/css3_image_filters.asp) to consider.

```css
.wilted   { filter: grayscale(0.8) brightness(0.7); }
.frosted  { filter: blur(2px) brightness(1.2); }
.ripened  { filter: saturate(1.5); }
```

### Layering

```css
.spreading {
  z-index: 10;       /* higher = sits on top */
  position: relative; /* needed for z-index to work */
}

.stable {
  position: fixed; /* element stays in place, does not move */
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

### The core mechanism: classes

The **simplest thing** for your tool to do is to add, remove, or toggle a *class* on an element. That class contains the CSS styling.

```javascript
element.classList.add("watered")     // add a class
element.classList.remove("dormant")  // remove a class
element.classList.toggle("blooming") // on if off, off if on
```

If your tool changes how something *looks* or *behaves*, this is probably the only JS you need; you would define the look/behavior *in CSS*.

### Creating + Adding

If your tool adds something new to the page:

```javascript
const newPlant = document.createElement("div")  // make a new element
newPlant.classList.add("seedling") // "seedling" would be a CSS class
target.appendChild(newPlant) // place it inside another element (target)
```

### Changing content

If your tool changes the words inside something:

```javascript
element.textContent = "a new thought"     // changes the text
element.innerHTML = "<em>a new thought</em>"  // allows HTML tags inside
```

### Direct style changes

Usually CSS classes are cleaner, but sometimes you want to set one specific style directly:

```javascript
element.style.opacity = "0.5"
element.style.transform = "scale(1.2)"
element.style.fontSize = "12px"
element.style.color = "#ff00ff"
```

### Changing attributes

Useful for swapping an image, or changing a link:

```javascript
element.setAttribute("src", "new-image.png")
element.setAttribute("href", "https://example.com")
```

### Finding elements

```javascript
document.getElementById("plot-001")   // find one specific element
document.querySelector(".plot")       // find the first match
document.querySelectorAll(".plot")    // find all matches
```

---

## The pattern, start to finish

```javascript
// JS: what triggers it, and what it does
toolElement.addEventListener("click", () => {
  target.classList.remove("dormant")
  target.classList.add("watered")
})
```

```css
/* CSS: what that change actually looks like */
.watered {
  background-color: #d4ecdb;
  transition: background-color 0.6s ease;
}
```

That's the whole loop: **a trigger → a class change → a style.** Everything else is detail.

---

## Stuck? Try this order

1. Open the browser console (right-click → Inspect → Console tab) and look for red errors
2. Check that your class name matches exactly in both the JS and the CSS — typos are the #1 culprit
3. Check that the element ID you're targeting actually exists in the HTML
4. Ask a neighbor
5. Ask Nicci
