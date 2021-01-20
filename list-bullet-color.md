# How to change list bullet color

## Requirements

- Code editor
- `CSS`
- `HTML`

## Introduction

As you're designing a website, you probably wondered if you could change the color of unordered lists bullet. You might have tried several ways and nothing seems to work, but theres a light at the end of the tunnel, my friend 😂.

As I implemented here in this blog as such:

- List item one
- List item two
- List item three

## Code

### CSS Way

You can get more control over the styles of a list if you use:

```css
list-style: url(bullet.png);
```

That will give you the ability to change color and shape of the bullet. But if you want a simple bullet with just a different color you can style like this:

```css
ul {
  list-style: none;
}
```

Then you can create your own bullet:

```css
ul li::before {
  content: "•";
  color: tomato;
  display: inline-block;
  width: 1rem;
  margin-left: -1rem;
}
```

The `display`, `width` and `margin-left` part is necessary because we need to move the bullet to the left, since the **new** bullet is not in the same place as the original bullet was. We create a size `width` and move it to the left by its own size `margin-left: -1rem`.

### Markup and CSS Way

What makes this situation more complicated to deal with is the fact that the bullet and the text is in the same element `li`, so by that logic you can assume that if we create another element between those, the complication can no longer be.

Markup:

```html
<ul>
  <li><span>List item one</span></li>
  <li><span>List item two</span></li>
  <li><span>List item three</span></li>
</ul>
```

CSS:

```css
li {
  color: tomato;
}
li span {
  color: black;
}
```

That simplifies everything, but is **not recommended** as your markup semantics gets thrown away.

## Additional Resources

- [W3 - CSS Lists ](https://www.w3schools.com/css/css_list.asp)
