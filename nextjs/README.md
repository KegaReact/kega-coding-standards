# Nextjs

## Table of Contents
  1. [Directory structure](#directory-structure)
  1. [File naming](#file-naming)
  1. [Server component](#server-component)
  1. [Client component](#client-component)

## Basic rules
- Keep your code clean and readable.

## Directory structure
  <a name="directory-structure"></a><a name="1.1"></a>
  - [1.1](#directory-structure) Main directory structure.

    ```
    .
    ├── ...
    ├── src
    │   ├── app            # Nextjs routing files & site structure
    │   ├── components     # Reusable components like ProductTile
    │   ├── elements       # Small dumb elements used to build components like Button/Icon
    │   ├── css            # Main css of the site
    │   ├── hooks          # Hooks directory
    │   ├── lib            # Library directory
    │   ├── modules        # Modules larger components
    │   ├── redux          # Redux directory
    │   └── utils          # Utils directory
    ├── config             # Site config
    ├── translations       # Translations files
    └── ...
    ```

  <a name="app-directory-structure"></a><a name="1.2"></a>
  - [1.2](#app-directory-structure) App structrue of a basic ecom project.
    
    ```
    .
    ├── ...
    ├── app
    │   └── [storeCode]
    │       ├── (default)
    │       │   ├── (home)
    │       │   ├── [...contentSlugs]
    │       │   ├── c
    │       │   ├── p
    │       │   └── customer
    │       └── (minimal)
    │           └── Checkout
    └── ...
    ```
  <a name="page-directory-structure"></a><a name="1.3"></a>
  - [1.3](#page-directory-structure) Page directory structure

    ```
    .
    ├── ...
    ├── [...contentSlugs]
    │   ├── page.js
    │   ├── page.module.css
    │   └── view
    │       ├── content
    │       │   ├── Content.js
    │       │   └── Content.module.css
    │       └── prductlist
    │           ├── ProductList.js
    │           └── ProductList.module.css
    └── ...
    ```
  <a name="layout-directory-structure"></a><a name="1.4"></a>
  - [1.4](#layout-directory-structure) Layout directory structure

    ```
    .
    ├── ...
    ├── app
    │   └── [storeCode]
    │       ├── (default)
    │       │   ├── layout.js
    │       │   ├── layout.module.css
    │       │   └── layout
    │       │       └── header
    │       │       │   ├── Header.js
    │       │       │   └── Header.module.css
    │       │       └── footer
    │       │           ├── Footer.js
    │       │           └── Footer.module.css
    │       └── (minimal)
    │           ├── layout.js
    │           ├── layout.module.css
    │           └── layout
    │               └── header
    │                   ├── MinimalHeader.js
    │                   └── MinimalHeader.module.css
    └── ...
    ```
  <a name="module-directory-structure"></a><a name="1.5"></a>
  - [1.5](#module-directory-structure) Module directory structure

    ```
    .
    ├── ...
    ├── src
    │   ├── app
    │   └── modules
    │       └── algolia
    │           ├── api
    │           ├── geolocation
    │           ├── instantsearch
    │           └── recommendations
    │   
    └── ...
    ``` 
    
## File naming
  <a name="file-naming"></a><a name="2.1"></a>
  - [2.1](#file-naming) File naming
    Nextjs has reserved names for specific files like layout.js, page.js, error.js , ...
    
    ```
    // bad
    .
    ├── ...
    ├── app
    │   └── [storeCode]
    │       └── account
    │           ├── details
    │           ├── Navigation.module.css
    │           ├── layout.js
    │           ├── page.js
    │           └── OverviewPage.module.css
    │           
    └── ...

    // good
    .
    ├── ...
    ├── app
    │   └── [storeCode]
    │       └── account
    │           ├── details
    │           ├── layout.module.css
    │           ├── layout.js
    │           ├── page.js
    │           └── page.module.css
    │           
    └── ...
    ```
    > This way the file/dir structure stays clear and its easy to spot witch css file belongs to witch js file.
  
  <a name="component-naming"></a><a name="2.2"></a>
  - [2.2](#component-naming) Component naming of reserved files (page.js)

    The problem in Nextjs is ther wil be a lot of the same file names page.js this wil make it hard to se witch file is open in youre code editor, so to clarify this give the component the name it represents.
  
    ```javascript
    
    // page.js
    import classes from './page.module.css';
    
    cons HomePage = () => {
    }
    
    ```
    
## Server component
  <a name="server-component"></a><a name="3"></a>
  - [3](#server-component) Server component
    
    Server Components are components that are rendered exclusively on the server and sent to the client as HTML the JavaScript wil not be send to the client.

    When loading async data in a Server Components the server wil wait until the date is loaded en serve the HTML to the client. This can cause slow loading page's.
    To prevent this use a good chaching strategy or wrap the server component in a suspense so the HTML gets streamd to the client.

    Server Components wil run only once on the server and do not have state so you can't use useState of useEffect
    
    Keep in mind when u use a Server Components in a Client Components the Server Components wil no longer be a Server Components and the js wil be send to de client.
    

## Client component
  <a name="client-component"></a><a name="4"></a>
  - [4](#client-component) Client component

    Client Components is a slightly confusing discritpion of what this component is, it is not a component that only runs in the browser. A Client Components first runs on the server to produce the HTML for server side rendering en wil be send to the client aling with the JavaScript of the component.

    There are ways to only run a Client Components on the browser this wil show up later in the browser so keep in mind ta add a fallback or loading state so it not causes unwanted behavior.
    
## Documentation
Official [Nextjs](https://nextjs.org/docs) documentation.

## Resources
[https://nextjs.org/blog](https://nextjs.org/blog)

