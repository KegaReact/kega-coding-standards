# Javascript

## Table of Contents
  1. [Whitespace](#whitespace)
  1. [Variable](#variable)
  1. [Semicolons and Quotes](#semicolons-and-quotes)

  ## Whitespace
  <a name="whitespace--spaces"></a><a name="1.1"></a>
  - [1.1](#whitespace--spaces) Use soft tabs (space character) set to 4 spaces. eslint: [`indent`](https://eslint.org/docs/rules/indent)
   
    > Why? Keeps the code consistent over all developer.

    ```javascript
    // bad
    const foo = () => {
    ∙∙let name;
    }

    // good
    const bar = () => {
    ∙∙∙∙let name;
    }
    ```
    
  ## Variable
  <a name="variables--const"></a><a name="2.1"></a>
  - [2.1](#variables--const) Always use `const` or `let` to declare variables. avoid using `var`. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign)

    > Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

    ```javascript
    // bad
    var a = 1;

    // good
    const a = 1;
    ```
    
    <a name="references--block-scope"></a><a name="2.2"></a>
  - [2.2](#references--block-scope) Note that both `let` and `const` are block-scoped, whereas `var` is function-scoped.

    > Why? `const` and `let` only exist in the blocks they are defined in.

    ```javascript
    {
      let a = 1;
      const b = 1;
      var c = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    console.log(c); // Prints 1
    ```
  <a name="variables--const-let-group"></a><a name="2.3"></a>
  - [2.3](#variables--const-let-group) Group all your `const`s and then group all your `let`s.

    > Why? It makes the code more readable.

    ```javascript
    // bad
    let i;
    const items = [];
    let other;
    const bar = true;
    let length;

    // good
    const items = [];
    const bar = true;
    
    let i;
    let other;
    let length;
    ```

    **[⬆ back to top](#table-of-contents)**

## Semicolons and Quotes
<a name="semicolons--required"></a><a name="3.1"></a>
- [3.1](#semicolons--required) Always add a `;` at the end of a line. eslint: [`semi`](https://eslint.org/docs/rules/semi)

   > Why? When JavaScript encounters a line break without a semicolon, it uses a set of rules called [Automatic Semicolon Insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) to determine whether it should regard that line break as the end of a statement.

  ```javascript
  //bad
  const object = {}
  const arr = []
  let text = 'test'

  arr.forEach(() => {
  })

  //good
  const object = {};
  const arr = [];
  let text = 'test';
  
  arr.forEach(() => {
  });
  
  const func = () => {
  }
  ```
<a name="quotes"></a><a name="3.2"></a>
- [3.2](#quotes) Use single quotes `''` for strings. eslint: [`quotes`](https://eslint.org/docs/rules/quotes)

  > Why? 
  ```javascript
  // bad
  const name = "Tim";

  // bad - template literals should contain interpolation or newlines
  const name = `Tim`;

  // good
  const name = 'Tim';
  const name = `Tim ${variable}`;

  const description = `Long text
  with newline`;
  ```

**[⬆ back to top](#table-of-contents)**
