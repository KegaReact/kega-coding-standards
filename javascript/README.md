# Javascript

## Table of Contents
  1. [Variable](#variable)

  ## Variable
	  <a name="variables--const"></a><a name="1.1"></a>
		- [1.1](#variables--const) Always use `const` or `let` to declare variables. avoid using `var`. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign)

  	> Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

    ```javascript
      // bad
    var a = 1;
 
    // good
    const a = 1;
    ```
