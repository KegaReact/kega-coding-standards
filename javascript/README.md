# Javascript

## Table of Contents
  1. [Whitespace](#whitespace)
  1. [Variable](#variable)
  1. [Semicolons and Quotes](#semicolons-and-quotes)
  1. [Naming Conventions](#naming-conventions)
  1. [Functions](#functions)
  1. [Destructuring](#destructuring)
  1. [Comparison Operators & Equality](#comparison-operators--equality)]
     
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

## Naming Conventions

<a name="naming--descriptive"></a><a name="4.1"></a>
  - [4.1](#naming--descriptive) Use descriptive variable and function names.
    
    > Why? It is clear for other developers it is clear when the variable or function is for.

<a name="naming--PascalCase"></a><a name="4.2"></a>
- [4.2](#naming--PascalCase) Use PascalCase only when naming constructors or classes. eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap)
    
    ```javascript
    // bad
    const events = () => {
        return {};
    });

    const events = new event();

    // good
    const Events = () => {
        return {};
    });

    const events = new Event();

    Event.js
    
    ```

<a name="naming--camelCase-default-export"></a><a name="4.3"></a>
- [4.3](#naming--camelCase-default-export) Use camelCase for functions, variables and filenames. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase)
    
    ```javascript
    // bad
    const long_variable_name = 0;

    const functions_name = () => {}

    functions_name.js

    // good
    const longVariableName = 0;

    const functionsName = () => {}

    functionsName.js
    ```

<a name="naming--filename-matches-export"></a><a name="4.4"></a>
- [4.4](#naming--filename-matches-export) A base filename should exactly match the name of its default export.

    ```javascript
    // bad
    import FunctionsName from './functionsName';
    import className from './ClassName';

    // good
    import functionsName from './functionsName';
    import ClassName from './ClassName';
    ```
    
<a name="naming--directories"></a><a name="4.5"></a>
- [4.5](#naming--directories) Do not use camelCase or PascalCase for filenames

    ```javascript
    // bad
    ./functionsName/functionsName.js
    ./ClassName/ClassName.js
    
    // good
    ./functions_name/functionsName.js
    ./class_name/ClassName.js
    ```
    **[⬆ back to top](#table-of-contents)**

## Functions

<a name="functions--declarations"></a><a name="5.1"></a>
  - [5.1](#functions--declarations) Function declarations.

    ```javascript
    // bad
    function foo() {
    }

    // good
    const foo = () => {
    }
    ```
    
    **[⬆ back to top](#table-of-contents)**


