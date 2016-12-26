# oneLogin HTML guide

## Table of Contents

1. [Syntax](#syntax)
2. [Attribute order](#attribute-order)
3. [Boolean attributes](#boolean-attributes)
4. [Reducing Markup](#reducing-markup)
5. [Comments](#comments)
6. [Loading Files](#loading-files)



### Syntax
* Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment.
* Use lowercase elements. `<li></li>`
* Use lowercase attribute names. ` <img src="">`
* Do not add blank lines without a reason.
* For readability, add blank lines to separate large or logical code blocks.
* Nested elements should be indented once (two spaces).
* Always use double quotes, never single quotes, on attributes 
* Don't include a trailing slash in self-closing elements—the HTML5 spec says they're optional (e.g. `<img>`).
* When using an HTML editor, it is inconvenient to scroll right and left to read the HTML code.
* Don’t omit optional closing tags (e.g. `</li>` or `</body>`).

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
```

* HTML5 allows spaces around equal signs. But space-less is easier to read, and groups entities better together.
```html
<!-- Bad Example -->
<link rel = "stylesheet" href = "styles.css">

<!-- Good Example -->
<link rel="stylesheet" href="styles.css">
```


### Attribute Order
HTML attributes should come in this particular order for easier reading of code.

* `class`
* `id`, `name`
* `data-*`
* `src`, `for`, `type`, `href`, `value`
* `title`, `alt`
* `role`, `aria-*`

Classes make for great reusable components, so they come first. Ids are more specific and should be used sparingly (e.g., for in-page bookmarks), so they come second.
```html
<a class="..." id="..." data-toggle="modal" href="#">
  Example link
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```
### Boolean Attributes

* A boolean attribute is one that needs no declared value.
* The presence of a boolean attribute on an element represents the true value, and the absence of the attribute represents the false value.
* They should be the last written attributes in HTML element.

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

### Reducing Markup
Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML.

```html
<!-- Bad Example -->
<span class="avatar">
  <img src="...">
</span>

<!-- Good Example-->
<img class="avatar" src="...">
```

### Comments
* Short comments should be written on one line, like this:
``` html
<!-- This is a comment -->
```
* Comments that spans more than one line, should be written like this:
```html 
<!-- 
  This is a long comment example. This is a long comment example.
  This is a long comment example. This is a long comment example.
-->
```

### Loading files
* CSS Files should be loaded in the `<head>` tag.
* Javascript files should be loaded at the bottom of the `<body>` tag so that the HTML and CSS are loaded first.