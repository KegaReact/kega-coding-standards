# React

## Table of Contents
  1. [Test](#test)

  ## Test

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
