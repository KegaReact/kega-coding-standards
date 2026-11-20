# Typescript

This standard builds on the [Javascript](../javascript/) standard. Everything in the Javascript standard also applies to TypeScript. This document shows the TypeScript version of those rules and adds rules that only exist in TypeScript.

## Table of Contents
  1. [Whitespace](#whitespace)
  1. [Variable](#variable)
  1. [Semicolons and Quotes](#semicolons-and-quotes)
  1. [Naming Conventions](#naming-conventions)
  1. [Functions](#functions)
  1. [Destructuring](#destructuring)
  1. [Comparison Operators & Equality](#comparison-operators--equality)
  1. [Compiler Settings](#compiler-settings)
  1. [Types vs Interfaces](#types-vs-interfaces)
  1. [Any, Unknown and Assertions](#any-unknown-and-assertions)
  1. [Enums](#enums)
  1. [Imports & Exports](#imports--exports)
  1. [Narrowing & Unions](#narrowing--unions)
  1. [Generics & Utility Types](#generics--utility-types)
  1. [Runtime Validation](#runtime-validation)
  1. [Linting](#linting)

## Whitespace
  <a name="whitespace--spaces"></a><a name="1.1"></a>
  - [1.1](#whitespace--spaces) Use soft tabs (space character) set to 4 spaces. eslint: [`@stylistic/indent`](https://eslint.style/rules/indent)

    > Why? Keeps the code consistent over all developers.

    ```typescript
    // bad
    const foo = (): void => {
    ∙∙let name: string;
    };

    // good
    const bar = (): void => {
    ∙∙∙∙let name: string;
    };
    ```

  <a name="whitespace--padding"></a><a name="1.2"></a>
  - [1.2](#whitespace--padding) Object & Array whitespace padding. This also counts for tuples and destructuring. eslint: [`@stylistic/list-style`](https://eslint.style/rules/list-style), [`@stylistic/comma-spacing`](https://eslint.style/rules/comma-spacing)

    > Why? Keeps the code easy to read.

    ```typescript
    // bad
    const object = {attr:'value',attr2:'value2'};
    const array = [0,1,2,3];

    // good
    const object = { attr: 'value', attr2: 'value2' };
    const array = [ 0, 1, 2, 3 ];
    ```

  <a name="whitespace--type-annotation"></a><a name="1.3"></a>
  - [1.3](#whitespace--type-annotation) Use one space after the colon of a type, and no space before it. Use a space around the arrow of a function type. eslint: [`@stylistic/type-annotation-spacing`](https://eslint.style/rules/type-annotation-spacing)

    > Why? Types are read a lot, the same spacing everywhere makes them easy to scan.

    ```typescript
    // bad
    const name:string = 'Tim';
    const getName = (user : User):string => user.name;
    type OnClick = (event: MouseEvent)=>void;

    // good
    const name: string = 'Tim';
    const getName = (user: User): string => user.name;
    type OnClick = (event: MouseEvent) => void;
    ```

  **[⬆ back to top](#table-of-contents)**

## Variable
  <a name="variables--const"></a><a name="2.1"></a>
  - [2.1](#variables--const) Always use `const` or `let` to declare variables. Never use `var`. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const), [`no-var`](https://eslint.org/docs/rules/no-var)

    > Why? See [Javascript 2.1](../javascript/#variables--const). This rule is the same in TypeScript.

    ```typescript
    // bad
    var a = 1;

    // good
    const a = 1;
    ```

  <a name="variables--inference"></a><a name="2.2"></a>
  - [2.2](#variables--inference) Let TypeScript work out the type when it is obvious. Do not add a type to a variable that gets a simple value. eslint: [`@typescript-eslint/no-inferrable-types`](https://typescript-eslint.io/rules/no-inferrable-types)

    > Why? TypeScript already knows `0` is a `number`. Writing it again only adds noise.

    ```typescript
    // bad
    const count: number = 0;
    const name: string = 'Tim';
    const isOpen: boolean = false;

    // good
    const count = 0;
    const name = 'Tim';
    const isOpen = false;
    ```

  <a name="variables--empty"></a><a name="2.3"></a>
  - [2.3](#variables--empty) Do add a type when TypeScript can not work it out, like an empty array or a `let` without a value.

    > Why? An empty array without a type can not hold anything useful, and a `let` without a value becomes `any`.

    ```typescript
    // bad
    const products = [];
    let total;

    // good
    const products: Product[] = [];
    let total: number;
    ```

  <a name="variables--as-const"></a><a name="2.4"></a>
  - [2.4](#variables--as-const) Use `as const` for values that never change.

    > Why? TypeScript then knows the exact values and makes them read-only.

    ```typescript
    // bad
    const sizes = [ 'small', 'medium', 'large' ]; // string[]

    // good
    const sizes = [ 'small', 'medium', 'large' ] as const; // readonly ['small', 'medium', 'large']
    ```

  <a name="variables--const-let-group"></a><a name="2.5"></a>
  - [2.5](#variables--const-let-group) Group all your `const`s and then group all your `let`s.

    > Why? It makes the code more readable.

    ```typescript
    // bad
    let i: number;
    const items: Item[] = [];
    let other: string;
    const bar = true;

    // good
    const items: Item[] = [];
    const bar = true;

    let i: number;
    let other: string;
    ```

  **[⬆ back to top](#table-of-contents)**

## Semicolons and Quotes
  <a name="semicolons--required"></a><a name="3.1"></a>
  - [3.1](#semicolons--required) Always add a `;` at the end of a line. eslint: [`@stylistic/semi`](https://eslint.style/rules/semi)

    > Why? See [Javascript 3.1](../javascript/#semicolons--required).

    ```typescript
    // bad
    const object = {}
    let text = 'test'

    // good
    const object = {};
    let text = 'test';
    ```

  <a name="quotes"></a><a name="3.2"></a>
  - [3.2](#quotes) Use single quotes `''` for strings. Only use template literals for interpolation or newlines. eslint: [`@stylistic/quotes`](https://eslint.style/rules/quotes)

    ```typescript
    // bad
    const name = "Tim";
    const name = `Tim`;

    // good
    const name = 'Tim';
    const name = `Tim ${lastName}`;
    ```

  <a name="semicolons--members"></a><a name="3.3"></a>
  - [3.3](#semicolons--members) End every member of an interface or type with a `;`. eslint: [`@stylistic/member-delimiter-style`](https://eslint.style/rules/member-delimiter-style)

    > Why? It looks the same as the end of a line in normal code.

    ```typescript
    // bad
    interface User {
        firstName: string,
        lastName: string
    }

    // good
    interface User {
        firstName: string;
        lastName: string;
    }
    ```

  **[⬆ back to top](#table-of-contents)**

## Naming Conventions
  <a name="naming--descriptive"></a><a name="4.1"></a>
  - [4.1](#naming--descriptive) Use descriptive names for variables, functions and types.

    > Why? Other developers can see what a variable, function or type is for.

  <a name="naming--camelCase"></a><a name="4.2"></a>
  - [4.2](#naming--camelCase) Use camelCase for variables, functions and parameters. eslint: [`@typescript-eslint/naming-convention`](https://typescript-eslint.io/rules/naming-convention)

    ```typescript
    // bad
    const long_variable_name = 0;
    const functions_name = (): void => {};

    // good
    const longVariableName = 0;
    const functionsName = (): void => {};
    ```

  <a name="naming--PascalCase"></a><a name="4.3"></a>
  - [4.3](#naming--PascalCase) Use PascalCase for classes, interfaces, types and React components. eslint: [`@typescript-eslint/naming-convention`](https://typescript-eslint.io/rules/naming-convention)

    ```typescript
    // bad
    interface user {}
    type orderStatus = 'open' | 'paid';

    // good
    interface User {}
    type OrderStatus = 'open' | 'paid';
    ```

  <a name="naming--no-prefix"></a><a name="4.4"></a>
  - [4.4](#naming--no-prefix) Do not add a prefix or suffix to interfaces and types, like `I` or `Type`. eslint: [`@typescript-eslint/naming-convention`](https://typescript-eslint.io/rules/naming-convention)

    > Why? The editor already shows what something is. `User` is easier to read than `IUser` or `UserType`.

    ```typescript
    // bad
    interface IUser {}
    type UserType = {};

    // good
    interface User {}
    ```

  <a name="naming--generics"></a><a name="4.5"></a>
  - [4.5](#naming--generics) Name generics with a `T`. Use `T` alone when there is one, and `T` plus a name when there are more. eslint: [`@typescript-eslint/naming-convention`](https://typescript-eslint.io/rules/naming-convention)

    ```typescript
    // bad
    const first = <item>(list: item[]): item | undefined => list[0];
    const toMap = <A, B>(list: A[], getKey: (item: A) => B): Map<B, A> => {};

    // good
    const first = <T>(list: T[]): T | undefined => list[0];
    const toMap = <TItem, TKey>(list: TItem[], getKey: (item: TItem) => TKey): Map<TKey, TItem> => {};
    ```

  <a name="naming--files"></a><a name="4.6"></a>
  - [4.6](#naming--files) Use `.ts` for files and `.tsx` only for files with JSX. The filename and directory rules from the [Javascript standard](../javascript/#naming--filename-matches-export) stay the same.

    ```typescript
    // bad
    ./functions_name/functionsName.tsx // file without JSX
    ./product_card/ProductCard.ts      // file with JSX

    // good
    ./functions_name/functionsName.ts
    ./product_card/ProductCard.tsx
    ```

  **[⬆ back to top](#table-of-contents)**

## Functions
  <a name="functions--declarations"></a><a name="5.1"></a>
  - [5.1](#functions--declarations) Use arrow functions and give every parameter a type.

    > Why? TypeScript can not work out the type of a parameter. Without a type it becomes `any`.

    ```typescript
    // bad
    function getPrice(product) {
    }

    // good
    const getPrice = (product: Product): number => {
    };
    ```

  <a name="functions--return-type"></a><a name="5.2"></a>
  - [5.2](#functions--return-type) Give exported functions a return type. eslint: [`@typescript-eslint/explicit-module-boundary-types`](https://typescript-eslint.io/rules/explicit-module-boundary-types)

    > Why? The return type is a promise to the rest of the code. When you change the function by mistake, TypeScript shows the error inside the function, not in every file that uses it.

    ```typescript
    // bad
    export const getFullName = (user: User) => {
        return `${user.firstName} ${user.lastName}`;
    };

    // good
    export const getFullName = (user: User): string => {
        return `${user.firstName} ${user.lastName}`;
    };
    ```

  <a name="functions--default-values"></a><a name="5.3"></a>
  - [5.3](#functions--default-values) Use a default value instead of an optional parameter when there is a sensible default.

    > Why? With a default value the parameter is never `undefined` inside the function, so you do not need extra checks.

    ```typescript
    // bad
    const formatPrice = (price: number, currency?: string): string => {
        return `${price} ${currency ?? 'EUR'}`;
    };

    // good
    const formatPrice = (price: number, currency = 'EUR'): string => {
        return `${price} ${currency}`;
    };
    ```

  <a name="functions--promises"></a><a name="5.4"></a>
  - [5.4](#functions--promises) Always handle a promise. Use `await`, `.then()` / `.catch()`, or mark it on purpose with `void`. eslint: [`@typescript-eslint/no-floating-promises`](https://typescript-eslint.io/rules/no-floating-promises)

    > Why? A promise that is not handled can fail without anybody noticing.

    ```typescript
    // bad
    saveOrder(order);

    // good
    await saveOrder(order);

    // good - when you really do not want to wait
    void trackEvent('order_saved');
    ```

  **[⬆ back to top](#table-of-contents)**

## Destructuring
  <a name="destructuring--object"></a><a name="6.1"></a>
  - [6.1](#destructuring--object) Use object destructuring when accessing and using multiple properties of an object. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > Why? See [Javascript 6.1](../javascript/#destructuring--object).

    ```typescript
    // bad
    const getFullName = (user: User): string => {
        const firstName = user.firstName;
        const lastName = user.lastName;

        return `${firstName} ${lastName}`;
    };

    // good
    const getFullName = (user: User): string => {
        const { firstName, lastName } = user;
        return `${firstName} ${lastName}`;
    };

    // best
    const getFullName = ({ firstName, lastName }: User): string => {
        return `${firstName} ${lastName}`;
    };
    ```

  <a name="destructuring--parameter-type"></a><a name="6.2"></a>
  - [6.2](#destructuring--parameter-type) Put the type after the destructured parameter, not on each property. Use an interface when there are more than a few properties.

    > Why? The type is easier to read and can be used again.

    ```typescript
    // bad
    const Button = ({ label, onClick }: { label: string, onClick: () => void, disabled?: boolean, size?: 'small' | 'large' }) => {};

    // good
    interface ButtonProps {
        label: string;
        onClick: () => void;
        disabled?: boolean;
        size?: 'small' | 'large';
    }

    const Button = ({ label, onClick, disabled = false, size = 'small' }: ButtonProps) => {};
    ```

  <a name="destructuring--array"></a><a name="6.3"></a>
  - [6.3](#destructuring--array) Use array destructuring. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    ```typescript
    const arr = [ 1, 2, 3, 4 ];

    // bad
    const first = arr[0];
    const second = arr[1];

    // good
    const [ first, second ] = arr; // number | undefined, see 8.2
    ```

  <a name="destructuring--object-fallback"></a><a name="6.4"></a>
  - [6.4](#destructuring--object-fallback) Use fallback values when the object can be `undefined`.

    > Why? Destructuring `undefined` crashes the application. TypeScript shows this error, a fallback solves it.

    ```typescript
    const user: User | undefined = getUser();

    // bad
    const { firstName, lastName } = user; // Property 'firstName' does not exist on type 'User | undefined'.

    // good
    const { firstName = '', lastName = '' } = user ?? {};
    ```

  <a name="destructuring--object-alias"></a><a name="6.5"></a>
  - [6.5](#destructuring--object-alias) Use aliases when there is a name collision.

    ```typescript
    const { firstName: customerFirstName, lastName = '' } = customer ?? {};
    ```

  **[⬆ back to top](#table-of-contents)**

## Comparison Operators & Equality
  <a name="comparison--eqeqeq"></a><a name="7.1"></a>
  - [7.1](#comparison--eqeqeq) Use `===` and `!==` over `==` and `!=`. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq)

  <a name="comparison--shortcuts"></a><a name="7.2"></a>
  - [7.2](#comparison--shortcuts) Use shortcuts for booleans, but explicit comparisons for strings and numbers. eslint: [`@typescript-eslint/strict-boolean-expressions`](https://typescript-eslint.io/rules/strict-boolean-expressions)

    > Why? Same as [Javascript 7.3](../javascript/#comparison--shortcuts). In TypeScript the linter checks this for you, because it knows the type of every value.

    ```typescript
    // bad
    if (isValid === true) {}
    if (name) {}
    if (collection.length) {}

    // good
    if (isValid) {}
    if (name !== '') {}
    if (collection.length > 0) {}
    ```

  <a name="comparison--nested-ternaries"></a><a name="7.3"></a>
  - [7.3](#comparison--nested-ternaries) Ternaries should not be nested and generally be single line expressions. eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary), [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary)

    > Why? See [Javascript 7.4](../javascript/#comparison--nested-ternaries).

  <a name="comparison--nullish"></a><a name="7.4"></a>
  - [7.4](#comparison--nullish) Use `??` instead of `||` for fallback values. eslint: [`@typescript-eslint/prefer-nullish-coalescing`](https://typescript-eslint.io/rules/prefer-nullish-coalescing)

    > Why? `||` also replaces `0`, `''` and `false`. `??` only replaces `null` and `undefined`.

    ```typescript
    interface Product {
        quantity?: number;
    }

    // bad
    const quantity = product.quantity || 1; // 0 becomes 1

    // good
    const quantity = product.quantity ?? 1; // 0 stays 0
    ```

  <a name="comparison--optional-chaining"></a><a name="7.5"></a>
  - [7.5](#comparison--optional-chaining) Use optional chaining `?.` instead of `&&` checks. eslint: [`@typescript-eslint/prefer-optional-chain`](https://typescript-eslint.io/rules/prefer-optional-chain)

    ```typescript
    // bad
    const city = user && user.address && user.address.city;

    // good
    const city = user?.address?.city;
    ```

  <a name="comparison--non-null"></a><a name="7.6"></a>
  - [7.6](#comparison--non-null) Do not use the non-null assertion `!`. Check the value instead. eslint: [`@typescript-eslint/no-non-null-assertion`](https://typescript-eslint.io/rules/no-non-null-assertion)

    > Why? `!` tells TypeScript "trust me, this is not `null`". When you are wrong, the application crashes and TypeScript can not warn you.

    ```typescript
    // bad
    const button = document.querySelector('button')!;
    button.focus();

    // good
    const button = document.querySelector('button');
    button?.focus();
    ```

  **[⬆ back to top](#table-of-contents)**

## Compiler Settings
  <a name="compiler--strict"></a><a name="8.1"></a>
  - [8.1](#compiler--strict) Always use `strict` mode. Start every project with these settings in `tsconfig.json`.

    > Why? Without `strict`, TypeScript misses most of the bugs it is made for, like values that can be `null` or `undefined`.

    ```json
    {
        "compilerOptions": {
            "strict": true,
            "noUncheckedIndexedAccess": true,
            "noImplicitOverride": true,
            "noFallthroughCasesInSwitch": true,
            "verbatimModuleSyntax": true,
            "isolatedModules": true,
            "erasableSyntaxOnly": true,
            "skipLibCheck": true
        }
    }
    ```

    Frameworks like Next.js create a `tsconfig.json` for you. Keep it and add the settings above that are missing.

  <a name="compiler--indexed-access"></a><a name="8.2"></a>
  - [8.2](#compiler--indexed-access) `noUncheckedIndexedAccess` adds `undefined` to every value you get from an array or object by index.

    > Why? An array can be empty and an object can miss a key. This setting makes you check it.

    ```typescript
    const products: Product[] = [];

    // bad - crashes, products[0] is undefined
    const name = products[0].name;

    // good
    const name = products[0]?.name ?? '';
    ```

  <a name="compiler--erasable"></a><a name="8.3"></a>
  - [8.3](#compiler--erasable) `verbatimModuleSyntax` and `erasableSyntaxOnly` only allow TypeScript that can be removed to get plain Javascript. This blocks `enum`, `namespace` and constructor parameter properties.

    > Why? Tools like Node.js, Vite and Next.js remove the types without reading the rest of your code. Code that works this way runs the same everywhere.

    ```typescript
    // bad
    class Cart {
        constructor(private items: Item[]) {}
    }

    // good
    class Cart {
        private items: Item[];

        constructor(items: Item[]) {
            this.items = items;
        }
    }
    ```

  <a name="compiler--ts-comment"></a><a name="8.4"></a>
  - [8.4](#compiler--ts-comment) Do not use `// @ts-ignore`. When you really need to skip an error, use `// @ts-expect-error` with a reason. eslint: [`@typescript-eslint/ban-ts-comment`](https://typescript-eslint.io/rules/ban-ts-comment)

    > Why? `@ts-expect-error` gives an error itself when the problem is fixed, so the comment does not stay behind.

    ```typescript
    // bad
    // @ts-ignore
    legacyPlugin.init();

    // good
    // @ts-expect-error: legacy-plugin has no types for init(), remove when v3 is released
    legacyPlugin.init();
    ```

  **[⬆ back to top](#table-of-contents)**

## Types vs Interfaces
  <a name="types--interface"></a><a name="9.1"></a>
  - [9.1](#types--interface) Use `interface` for the shape of an object. eslint: [`@typescript-eslint/consistent-type-definitions`](https://typescript-eslint.io/rules/consistent-type-definitions)

    > Why? One way to write objects keeps the code consistent. Interfaces also give clearer error messages.

    ```typescript
    // bad
    type User = {
        firstName: string;
        lastName: string;
    };

    // good
    interface User {
        firstName: string;
        lastName: string;
    }
    ```

  <a name="types--type"></a><a name="9.2"></a>
  - [9.2](#types--type) Use `type` for everything an interface can not do, like unions, tuples, functions and utility types.

    ```typescript
    type OrderStatus = 'open' | 'paid' | 'shipped';
    type Coordinates = [ number, number ];
    type OnChange = (value: string) => void;
    type ProductPreview = Pick<Product, 'id' | 'name'>;
    ```

  <a name="types--extends"></a><a name="9.3"></a>
  - [9.3](#types--extends) Use `extends` to build an interface on top of another one.

    > Why? `extends` shows an error when the two types do not fit together. `&` silently creates a type that can never exist.

    ```typescript
    // bad
    type Customer = User & {
        customerNumber: string;
    };

    // good
    interface Customer extends User {
        customerNumber: string;
    }
    ```

  **[⬆ back to top](#table-of-contents)**

## Any, Unknown and Assertions
  <a name="any--no-any"></a><a name="10.1"></a>
  - [10.1](#any--no-any) Do not use `any`. Use `unknown` and check the type before you use it. eslint: [`@typescript-eslint/no-explicit-any`](https://typescript-eslint.io/rules/no-explicit-any)

    > Why? `any` turns TypeScript off for that value and for everything it touches. `unknown` makes you check the value first.

    ```typescript
    // bad
    const getMessage = (error: any): string => {
        return error.message;
    };

    // good
    const getMessage = (error: unknown): string => {
        if (error instanceof Error) {
            return error.message;
        }

        return 'Something went wrong';
    };
    ```

  <a name="any--assertions"></a><a name="10.2"></a>
  - [10.2](#any--assertions) Avoid type assertions with `as`. Only `as const` is fine. eslint: [`@typescript-eslint/consistent-type-assertions`](https://typescript-eslint.io/rules/consistent-type-assertions)

    > Why? `as` tells TypeScript to stop checking. When the data is different, you find out in production. Check the data instead, see [Runtime Validation](#runtime-validation).

    ```typescript
    // bad
    const user = await response.json() as User;

    // good
    const user = userSchema.parse(await response.json());
    ```

  <a name="any--satisfies"></a><a name="10.3"></a>
  - [10.3](#any--satisfies) Use `satisfies` to check a value against a type without losing the exact type.

    > Why? A type annotation makes the value as wide as the type. `satisfies` checks the value and keeps what TypeScript knows about it.

    ```typescript
    type Routes = Record<string, string>;

    // bad
    const routes: Routes = {
        home: '/',
        cart: '/cart',
    };
    routes.chekout; // no error, every key is allowed

    // good
    const routes = {
        home: '/',
        cart: '/cart',
    } satisfies Routes;
    routes.chekout; // error: Property 'chekout' does not exist
    ```

  **[⬆ back to top](#table-of-contents)**

## Enums
  <a name="enums--union"></a><a name="11.1"></a>
  - [11.1](#enums--union) Do not use `enum`. Use a union of strings.

    > Why? An `enum` is not plain Javascript and is blocked by `erasableSyntaxOnly` (see [8.3](#compiler--erasable)). A union does the same and has no runtime code.

    ```typescript
    // bad
    enum OrderStatus {
        Open = 'open',
        Paid = 'paid',
    }

    // good
    type OrderStatus = 'open' | 'paid';
    ```

  <a name="enums--as-const"></a><a name="11.2"></a>
  - [11.2](#enums--as-const) Use an `as const` object when you also need the values in your code, for example to loop over them. Get the type from the object.

    > Why? The values and the type come from one place, so they can not get out of sync.

    ```typescript
    const orderStatus = {
        open: 'open',
        paid: 'paid',
    } as const;

    type OrderStatus = typeof orderStatus[keyof typeof orderStatus]; // 'open' | 'paid'

    const statuses = Object.values(orderStatus); // [ 'open', 'paid' ]
    ```

  **[⬆ back to top](#table-of-contents)**

## Imports & Exports
  <a name="imports--type"></a><a name="12.1"></a>
  - [12.1](#imports--type) Use `import type` when you only import types. eslint: [`@typescript-eslint/consistent-type-imports`](https://typescript-eslint.io/rules/consistent-type-imports)

    > Why? Type imports are removed from the build. With `verbatimModuleSyntax` (see [8.1](#compiler--strict)) TypeScript requires it.

    ```typescript
    // bad
    import { User, getUser } from './user';

    // good
    import { getUser } from './user';
    import type { User } from './user';

    // good
    import { type User, getUser } from './user';
    ```

  <a name="imports--named-types"></a><a name="12.2"></a>
  - [12.2](#imports--named-types) Export types with a named export, next to the code that uses them. Only move a type to a shared `types.ts` file when more modules use it.

    > Why? A type next to its code is easy to find and is removed together with the code.

    ```typescript
    // good - ./product_card/ProductCard.tsx
    export interface ProductCardProps {
        product: Product;
    }

    const ProductCard = ({ product }: ProductCardProps) => {};

    export default ProductCard;
    ```

  **[⬆ back to top](#table-of-contents)**

## Narrowing & Unions
  <a name="narrowing--checks"></a><a name="13.1"></a>
  - [13.1](#narrowing--checks) Narrow a type with a check like `typeof`, `in` or `instanceof`, not with `as`.

    > Why? After the check TypeScript knows the type, and the check also works at runtime.

    ```typescript
    // bad
    const formatId = (id: string | number): string => {
        return (id as string).toUpperCase();
    };

    // good
    const formatId = (id: string | number): string => {
        if (typeof id === 'number') {
            return id.toString();
        }

        return id.toUpperCase();
    };
    ```

  <a name="narrowing--discriminated"></a><a name="13.2"></a>
  - [13.2](#narrowing--discriminated) Use a union with a shared property (a discriminated union) for things that can be in different states.

    > Why? Every state only has the properties that belong to it. You can not read `data` while it is still loading.

    ```typescript
    // bad
    interface RequestState {
        isLoading: boolean;
        data?: Product[];
        error?: string;
    }

    // good
    type RequestState =
        | { status: 'loading' }
        | { status: 'success'; data: Product[] }
        | { status: 'error'; error: string };
    ```

  <a name="narrowing--exhaustive"></a><a name="13.3"></a>
  - [13.3](#narrowing--exhaustive) Handle every case of a union in a `switch`. eslint: [`@typescript-eslint/switch-exhaustiveness-check`](https://typescript-eslint.io/rules/switch-exhaustiveness-check)

    > Why? When somebody adds a new state, TypeScript shows every `switch` that does not handle it yet.

    ```typescript
    const getLabel = (state: RequestState): string => {
        switch (state.status) {
            case 'loading':
                return 'Loading...';
            case 'success':
                return `${state.data.length} products`;
            case 'error':
                return state.error;
            default:
                return state satisfies never;
        }
    };
    ```

  **[⬆ back to top](#table-of-contents)**

## Generics & Utility Types
  <a name="generics--when"></a><a name="14.1"></a>
  - [14.1](#generics--when) Only use a generic when it connects types, for example the type that goes in with the type that comes out.

    > Why? A generic that is used once does not add anything and makes the function harder to read.

    ```typescript
    // bad - T is used once, this is the same as (value: unknown)
    const log = <T>(value: T): void => {
        console.log(value);
    };

    // good - the type that goes in is the type that comes out
    const first = <T>(list: T[]): T | undefined => list[0];
    ```

  <a name="generics--utility"></a><a name="14.2"></a>
  - [14.2](#generics--utility) Use utility types to build a type from another type instead of copying it.

    > Why? When the original type changes, the other types change with it.

    ```typescript
    // bad
    interface ProductPreview {
        id: string;
        name: string;
    }

    // good
    type ProductPreview = Pick<Product, 'id' | 'name'>;
    type ProductUpdate = Partial<Omit<Product, 'id'>>;
    type PricesBySku = Record<string, number>;
    ```

    The most used utility types are [`Partial`](https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype), [`Required`](https://www.typescriptlang.org/docs/handbook/utility-types.html#requiredtype), [`Pick`](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys), [`Omit`](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys), [`Record`](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type), [`ReturnType`](https://www.typescriptlang.org/docs/handbook/utility-types.html#returntypetype) and [`Awaited`](https://www.typescriptlang.org/docs/handbook/utility-types.html#awaitedtype).

  <a name="generics--record"></a><a name="14.3"></a>
  - [14.3](#generics--record) Use `Record` for objects with dynamic keys. eslint: [`@typescript-eslint/consistent-indexed-object-style`](https://typescript-eslint.io/rules/consistent-indexed-object-style)

    ```typescript
    // bad
    interface PricesBySku {
        [sku: string]: number;
    }

    // good
    type PricesBySku = Record<string, number>;
    ```

  **[⬆ back to top](#table-of-contents)**

## Runtime Validation
  <a name="validation--external"></a><a name="15.1"></a>
  - [15.1](#validation--external) Check all data from outside your code with [Zod](https://zod.dev), like API responses, form data and environment variables. Get the type from the schema with `z.infer`.

    > Why? TypeScript types are removed when the code runs. An API can return something else than your type says. Zod checks the data at runtime, and the schema and the type can not get out of sync.

    ```typescript
    import { z } from 'zod';

    // bad
    interface User {
        id: number;
        email: string;
    }

    const user = await response.json() as User;

    // good
    const userSchema = z.object({
        id: z.number(),
        email: z.email(),
    });

    type User = z.infer<typeof userSchema>;

    const user = userSchema.parse(await response.json());
    ```

  <a name="validation--safe-parse"></a><a name="15.2"></a>
  - [15.2](#validation--safe-parse) Use `safeParse` when invalid data is expected, like user input, and handle the error.

    > Why? `parse` throws an error. `safeParse` returns the result, so you can show a message instead of crashing.

    ```typescript
    const result = userSchema.safeParse(formData);

    if (!result.success) {
        return { errors: z.flattenError(result.error).fieldErrors };
    }

    const user = result.data;
    ```

  <a name="validation--env"></a><a name="15.3"></a>
  - [15.3](#validation--env) Check environment variables once when the application starts.

    > Why? A missing variable gives a clear error at startup, not a strange bug later.

    ```typescript
    const envSchema = z.object({
        API_URL: z.url(),
        API_KEY: z.string().min(1),
    });

    export const env = envSchema.parse(process.env);
    ```

  **[⬆ back to top](#table-of-contents)**

## Linting
  <a name="linting--config"></a><a name="16.1"></a>
  - [16.1](#linting--config) Use [typescript-eslint](https://typescript-eslint.io) with the `strictTypeChecked` and `stylisticTypeChecked` configs, and [ESLint Stylistic](https://eslint.style) for formatting. This config checks the rules in this document.

    ```javascript
    // eslint.config.mjs
    import eslint from '@eslint/js';
    import stylistic from '@stylistic/eslint-plugin';
    import { defineConfig } from 'eslint/config';
    import tseslint from 'typescript-eslint';

    export default defineConfig(
        eslint.configs.recommended,
        tseslint.configs.strictTypeChecked,
        tseslint.configs.stylisticTypeChecked,
        {
            languageOptions: {
                parserOptions: {
                    projectService: true,
                },
            },
            plugins: {
                '@stylistic': stylistic,
            },
            rules: {
                // Javascript rules
                'eqeqeq': 'error',
                'no-nested-ternary': 'error',
                'no-unneeded-ternary': 'error',
                'prefer-const': 'error',
                'prefer-destructuring': 'error',

                // Formatting
                '@stylistic/indent': [ 'error', 4 ],
                '@stylistic/list-style': [ 'error', {
                    singleLine: { spacing: 'never' },
                    overrides: {
                        '{}': { singleLine: { spacing: 'always' } },
                        '[]': { singleLine: { spacing: 'always' } },
                    },
                } ],
                '@stylistic/comma-spacing': 'error',
                '@stylistic/type-annotation-spacing': 'error',
                '@stylistic/semi': [ 'error', 'always' ],
                '@stylistic/quotes': [ 'error', 'single' ],
                '@stylistic/member-delimiter-style': 'error',

                // TypeScript rules
                '@typescript-eslint/consistent-type-imports': 'error',
                '@typescript-eslint/explicit-module-boundary-types': 'error',
                '@typescript-eslint/restrict-template-expressions': [ 'error', { allowNumber: true } ],
                '@typescript-eslint/strict-boolean-expressions': [ 'error', { allowString: false, allowNumber: false } ],
                '@typescript-eslint/switch-exhaustiveness-check': 'error',
                '@typescript-eslint/naming-convention': [
                    'error',
                    { selector: 'default', format: [ 'camelCase' ] },
                    { selector: [ 'variable', 'function' ], format: [ 'camelCase', 'PascalCase' ] },
                    { selector: 'typeLike', format: [ 'PascalCase' ] },
                    { selector: 'interface', format: [ 'PascalCase' ], custom: { regex: '^I[A-Z]', match: false } },
                    { selector: 'typeParameter', format: [ 'PascalCase' ], custom: { regex: '^T([A-Z]|$)', match: true } },
                    { selector: [ 'objectLiteralProperty', 'import' ], format: null },
                ],
            },
        },
    );
    ```

  <a name="linting--version"></a><a name="16.2"></a>
  - [16.2](#linting--version) TypeScript 7 is the new, much faster version of the compiler. typescript-eslint does not support it yet. Until it does, install TypeScript 6.0 in projects that use typescript-eslint. Check the [typescript-eslint dependency versions](https://typescript-eslint.io/users/dependency-versions) before you upgrade.

  **[⬆ back to top](#table-of-contents)**

## Documentation
Official [TypeScript](https://www.typescriptlang.org/docs/) documentation.

## Resources
- [TypeScript handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TSConfig reference](https://www.typescriptlang.org/tsconfig/)
- [typescript-eslint rules](https://typescript-eslint.io/rules/)
- [Zod](https://zod.dev)
