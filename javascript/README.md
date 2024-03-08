# Javascript

## Table of Contents
  1. [Whitespace](#whitespace)
  1. [Variable](#variable)
  1. [Semicolons and Quotes](#semicolons-and-quotes)
  1. [Naming Conventions](#naming-conventions)
  1. [Functions](#functions)
  1. [Destructuring](#destructuring)
  1. [Comparison Operators & Equality](#comparison-operators--equality)
     
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
  <a name="whitespace--padding"></a><a name="1.2"></a>
  - [1.2](#whitespace--padding) Object & Array whitspace padding
   
    > Why? Keeps the code easy to read.

    ```javascript
    // bad
    const object = {attr:'value',attr2:'value2'};
    const array = [0,1,2,3];

    // good
    const object = { attr:'value', attr2:'value2' };
    const array = [ 0, 1, 2, 3 ];
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

## Destructuring

  <a name="destructuring--object"></a><a name="6.1"></a>
  - [6.1](#destructuring--object) Use object destructuring when accessing and using multiple properties of an object. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > Why? Destructuring saves you from creating temporary references for those properties, and from repetitive access of the object. Repeating object access creates more repetitive code, requires more reading, and creates more opportunities for mistakes.
    
    ```javascript
    // bad
    const getFullName = (user) => {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // good
    const getFullName = (user) = {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // best
    const getFullName = ({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```
    
  <a name="destructuring--array"></a><a name="6.2"></a>
  - [6.2](#destructuring--array) Use array destructuring. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // bad
    const first = arr[0];
    const second = arr[1];

    // good
    const [ first, second ] = arr;
    ```
  <a name="destructuring--object"></a><a name="6.3"></a>
  - [6.3](#destructuring--object) Use object destructuring.

    ```javascript
    const user = { firstname: 'Tim', lastname: 'Honders' }

    // bad
    const firstname = user.firstname;
    const lastname = user.lastname;

    // good
    const { firstname, lastname } = user;
    ```
  <a name="destructuring--object-fallback"></a><a name="6.4"></a>
  - [6.4](#destructuring--object-fallback) Use fallback values when destructuring an object.

    > Why? When trying to destruct an object that is undefined it will generate an error and crash de application.

    ```javascript
    const user = undefined

    // bad
    const { firstname, lastname } = user; // Cannot destructure property 'firstname' of 'user' as it is undefined.
    
    // good
    const { firstname='', lastname='' } = user || {}; 
    ```
  <a name="destructuring--object-alias"></a><a name="6.5"></a>
  - [6.5](#destructuring--object-fallback) Use aliases when there is a name collision

    ```javascript
    const user = { firstname: 'Tim', lastname: 'Honders' }

    const { firstname: firtnameAlias, lastname='' } = user || {}; 
    ```

- For more information refer to [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
    
  **[⬆ back to top](#table-of-contents)**

## Comparison Operators & Equality

  <a name="comparison--eqeqeq"></a><a name="7.1"></a>
  - [7.1](#comparison--eqeqeq) Use `===` and `!==` over `==` and `!=`. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq)

  <a name="comparison--if"></a><a name="7.2"></a>
  - [7.2](#comparison--if) Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

    - **Objects** evaluate to **true**
    - **Array** evaluate to **true**
    - **Undefined** evaluates to **false**
    - **Null** evaluates to **false**
    - **Booleans** evaluate to **the value of the boolean**
    - **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
    - **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

  <a name="comparison--shortcuts"></a><a name="7.3"></a>
  - [7.3](#comparison--shortcuts) Use shortcuts for booleans, but explicit comparisons for strings and numbers.

    ```javascript
    // bad
    if (isValid === true) {}

    // good
    if (isValid) {}

    // bad
    if (name) {}

    // good
    if (name !== '') {}

    // bad
    if (collection.length) {}

    // good
    if (collection.length > 0) {}
    ```
  <a name="comparison--nested-ternaries"></a><a name="7.4"></a>
  - [7.4](#comparison--nested-ternaries) Ternaries should not be nested and generally be single line expressions. eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary)

    ```javascript
    // bad
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // split into 2 separated ternary expressions
    const maybeNull = value1 > value2 ? 'baz' : null;

    // better
    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // best
    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="7.5"></a>
  - [7.5](#comparison--unneeded-ternary) Avoid unneeded ternary statements. eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary)

    ```javascript
    // bad
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;
    const quux = a != null ? a : b;

    // good
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    const quux = a ?? b;
    ```
  <a name="nullish-coalescing-operator"><a name="7.5"></a>
  - [7.5](#nullish-coalescing-operator) The nullish coalescing operator (`??`) is a logical operator that returns its right-hand side operand when its left-hand side operand is `null` or `undefined`. Otherwise, it returns the left-hand side operand.

    > Why? It provides precision by distinguishing null/undefined from other falsy values, enhancing code clarity and predictability.

    ```javascript
    // bad
    const value = 0 ?? 'default';
    // returns 0, not 'default'

    // bad
    const value = '' ?? 'default';
    // returns '', not 'default'

    // good
    const value = null ?? 'default';
    // returns 'default'

    // good
    const user = {
      name: 'John',
      age: null
    };
    const age = user.age ?? 18;
    // returns 18
    ```
    
  <a name="comparison--object-attribute"><a name="7.6"></a>
  - [7.6](#comparison--object-attribute) Optional chaining (?.) check

    > Why? It provides a simple check to see if a object is not undefined and has a specific attribute 

    ```javascript

    const user = undefined;
    
    // bad
    console.log(user.firstname);

    // good
    if (user?.firstname) {
      console.log(user.firstname);
    }
  
    ```

    
