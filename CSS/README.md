# HTML/SASS Style guide

## Table of Contents
  1. [CSS](#css)
    - [Formatting](#formatting)
    - [Declaration order](#declaration-order)
    - [Prefixed properties](#prefixed-properties)
    - [Single Declarations](#single-declarations)
    - [Shorthand notation](#shorthand-notation)
    - [Class names](#class-names)
    - [Comments](#comments)
    - [JavaScript hooks](#javascript-hooks)
    - [Border](#border)
  2. [Sass](#sass)
    - [SASS Syntax](#sass-syntax)
    - [Variables](#variables)
    - [Extend directive](#extend-directive)
    - [Nesting](#nesting)
    - [Operators](#operators)

## CSS

### Formatting

* Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment.
* Prefer dashes over camelCasing in class names.
* Do not use ID selectors but if you using them Id Names should be in **lowerCamelCase**.
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace `{` in rule declarations
* In properties, put a space after, but not before, the `:` character.
* Put closing braces `}` of rule declarations on a new line
* End all declarations with a semi-colon. The last declaration's is optional, but your code is more error prone without it.
* Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
* Don't include spaces after commas within `rgb()`, `rgba()`, `hsl()`, `hsla()`, or `rect()` values.
* Lowercase all hex values, e.g. `#fff`.
* Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.
* Quote attribute values in selectors, `e.g., input[type="text"]`. They’re only optional in some cases, and it’s a good practice for consistency.
* Avoid specifying units for zero values, `e.g., margin: 0;` instead of `margin: 0px;`

```css
/* Bad Example */

.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}
```

```css
/* Good Example */

.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

### Declaration Order

Related property declarations should be grouped together following the order:

1. Positioning
2. Box model
3. Typographic
4. Visual
5. `@include` declarations
6. Nested Elements

Positioning comes first because it can remove an element from the normal flow of the document and override box model related styles. The box model comes next as it dictates a component's dimensions and placement.

Everything else takes place inside the component or without impacting the previous two sections, and thus they come last.

Grouping `@include`s at the end makes it easier to read the entire selector.

Nested selectors, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
  
  /* @includes declarations */
  @include transition(background 0.5s ease);
  

  /* Nested Elements */
  .nested-element{
     margin-right: 10px;
  }
}

```

### Prefixed Properties
When using vendor prefixed properties, indent each property such that the declaration's value lines up vertically for easy multi-line editing.

In Sublime Text 2, use **Selection → Add Previous Line `(⌃⇧↑)`** and **Selection → Add Next Line `(⌃⇧↓)`**.

```css
/* Prefixed properties */
.selector {
  -webkit-box-shadow: 0 1px 2px rgba(0,0,0,.15);
          box-shadow: 0 1px 2px rgba(0,0,0,.15);
}
```

### Single Declarations
In instances where a rule set includes only one declaration, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines.

```css
/* Single declarations on one line */
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

/* Multiple declarations, one per line */
.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url(../img/sprite.png);
}
```

### Shorthand Notation
Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values. Common overused shorthand properties include:

* `padding`
* `margin`
* `font`
* `background`
* `border`
* `border-radius`

Often times we don't need to set all the values a shorthand property represents. For example, HTML headings only set top and bottom margin, so when necessary, only override those two values. Excessive use of shorthand properties often leads to sloppier code with unnecessary overrides and unintended side effects.

```css
/* Bad example */
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

/* Good example */
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

### Class Names
* Keep classes lowercase and use dashes (not underscores or camelCase) (e.g., `.btn` and `.btn-danger`).
* Avoid excessive and arbitrary shorthand notation. `.btn` is useful for button, but .s doesn't mean anything.
* Keep classes as short and succinct as possible.
* Use meaningful names; use structural or purposeful names over presentational.
* Prefix classes based on the closest parent or base class.
* Use .js-* classes to denote behavior (as opposed to style), but keep these classes out of your CSS.

```css
/* Bad example */
.t { ... }
.red { ... }
.header { ... }

/* Good example */
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

### Selectors
* Use classes over generic element tag for optimum rendering performance but if tags were used should be in **lowercase**.
* Avoid using several attribute selectors (e.g., `[class^="..."]`) on commonly occuring components. Browser performance is known to be impacted by these.
* Keep selectors short and strive to limit the number of elements in each selector to three.
* Scope classes to the closest parent **only **when necessary (e.g., when not using prefixed classes).

```css
/* Bad example */
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

/* Good example */
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

### Comments

* Prefer comments on their own line. Avoid end-of-line comments.
* Write detailed comments for code that isn't self-documenting:
  - Compatibility or browser-specific hacks

**Comment structure**
```css
/*  ==============================================================================
    Section Comment Block
    ==========================================================================  */

/*  Sub Section Comment Block
    =========================================================================== */

/**
  * Short Description Comment
  */

/* Basic Comment */
```

### JavaScript Hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Border

Use `0` instead of `none` to specify that a style has no border.

```css
/* Bad Example */

.foo {
  border: none;
}
```

```css
/* Good Example */

.foo {
  border: 0;
}
```

## Sass

### SASS Syntax

* Use the `.scss` syntax, never the original `.sass` syntax.
* Order your regular CSS and `@include` declarations logically.

### Variables

* Prefer dash-cased variable names (e.g. `$my-variable`).
* Instead of describing what a variable looks like in the name, describe its function or purpose. In other words, try to choose semantic names for your variables.

```css
/* Bad Example */
$red: red;
$yellow: yellow;

/* Good Example */
$brand-color: red;
$accent-color: yellow;
```

### Extend directive

`@extend` should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). 

### Nesting

**Do not nest selectors more than three levels deep!**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

```css
// Without nesting
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// With nesting
.table > thead > tr {
  > th { … }
  > td { … }
}
```

### Operators
For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.

```css
/* Bad example */
.element {
  margin: 10px 0 $variable*2 10px;
}

/* Good example */
.element {
  margin: 10px 0 ($variable * 2) 10px;
}
```

