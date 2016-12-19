# Javascript Style Guide

## References

### Style Guides:
- [w3schools Style Guide](http://www.w3schools.com/js/js_conventions.asp)
- [Google Style Guide](https://google.github.io/styleguide/javascriptguide.xml)
- [Airbnb Style Guide](https://github.com/airbnb/javascript)

### Best practices:
- [W3.org javascript best practices](https://www.w3.org/wiki/JavaScript_best_practices)
- [W3 schools best practices](http://www.w3schools.com/js/js_best_practices.asp)

### General:
- [Javascript the right way](http://jstherightway.org/)
- [MDN Style guide writing](https://developer.mozilla.org/en-US/docs/MDN/Contribute/Guidelines/Writing_style_guide)

#Development Guides:

##Table of Contents:

 1. [File names](#files)
 1. [References](#references)
 1. [Objects, Arrays and Destruction](#objects)
 1. [Strings and Concatenations](#strings)
 1. [Functions and Arrow Functions](#functions)
 1. [Classes & Constructors (ES6 only)](#classes--constructors)
 1. [Modules (ES6 only)](#modules)
 1. [Variables](#variables)




 ## Types

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) **Primitives**: When you access a primitive type you work directly on its value.

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **Complex**: When you access a complex type you work on a reference to its value.

    + `object`
    + `array`
    + `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ back to top](#table-of-contents)**

