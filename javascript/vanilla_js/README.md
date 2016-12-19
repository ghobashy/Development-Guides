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




 ## References

  <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) Use `const` for all of your references; avoid using `var`. eslint: [`prefer-const`](http://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](http://eslint.org/docs/rules/no-const-assign.html)

    > Why? This ensures that you can't reassign your references, which can lead to bugs and difficult to comprehend code.

    ```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) If you must reassign references, use `let` instead of `var`. eslint: [`no-var`](http://eslint.org/docs/rules/no-var.html) jscs: [`disallowVar`](http://jscs.info/rule/disallowVar)

    > Why? `let` is block-scoped rather than function-scoped like `var`.

    ```javascript
    // bad
    var count = 1;
    if (true) {
      count += 1;
    }

    // good, use the let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) Note that both `let` and `const` are block-scoped.

    ```javascript
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

**[⬆ back to top](#table-of-contents)**





