# Nextjs

## Table of Contents
  1. [Directory structure](#directory-structure)
  1. [File naming](#file-naming)
  1. [Server component](#server-component)
  1. [Client component](#client-component)
  1. [2 Worlds (client/server)](#2-worlds)
  1. [Sharing data client/server](#sharing-data)

## Basic rules

## Directory structure
  <a name="directory-structure"></a><a name="1.1"></a>
  - [1.1](#directory-structure) Main directory structure.

    ```
    .
    ├── ...
    ├── src
    │   ├── app            # Nextjs routing files & site structure
    │   ├── components     # Reusable components lin eProductTile
    │   ├── config         # Site config
    │   ├── elements       # Small dumb elemnts used to build components like Button/Icon
    │   ├── css            # Main css of the site
    │   ├── hooks          # Hooks directory
    │   ├── lib            # Library directory
    │   ├── modules        # Modules larger components
    │   ├── redux          # Redux directory
    │   └── utils          # Utils directory
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

    There are 2 options we need to make a choice

    ```
    .
    ├── ...
    ├── [...contentSlugs]
    │   ├── page.js
    │   ├── page.module.css
    │   ├── content
    │   │   ├── Content.js
    │   │   └── Content.module.css
    │   └── prductlist
    │       ├── ProductList.js
    │       └── ProductList.module.css
    └── ...
    ```

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
    │           ├── Navigation.moduel.css
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
    │           ├── layout.moduel.css
    │           ├── layout.js
    │           ├── page.js
    │           └── page.module.css
    │           
    └── ...
    ```
    > This way the file/dir structure stays clear and its easy to spot witch css file belongs to witch js file.
  
  <a name="component-naming"></a><a name="2.2"></a>
  - [2.](#component-naming) Component naming of reserved files (page.js)

    There are 2 options we need to make a choice, in de js naming convention we decidet that the filenam needs to be te same as the Component name.
    The problem in Nextjs is ther wil be a lot of the same file names page.js this wil make it hard to se witch file is open in youre code editor.
    So we have 2 options:
    
    ```javascript
    
    // page.js
    import classes from './page.module.css';
    
    cons Page = () => {
    }
    
    ```

    ```javascript
    
    // page.js
    import classes from './page.module.css';
    
    cons HomePage = () => {
    }
    
    ```
    
## Server component
  <a name="server-component"></a><a name="3.1"></a>
  - [3.1](#server-component) Server component
    
    Server Components are components that are rendered exclusively on the server and sent to the client as HTML. They enable developers to write components that can directly access server-side data sources, and their code is not included in the client-side JavaScript bundle. This can lead to performance improvements, as less JavaScript needs to be downloaded, parsed, and executed on the client. However, since they're rendered on the server, they cannot handle user interactions or have state. They are intended to be used alongside traditional client components to create a balance between performance and interactivity.

## Client component
  <a name="client-component"></a><a name="4.1"></a>
  - [4.1](#client-component) Client component

    Client Components are components that run in the browser. They can maintain their own state, handle user interactions, and can be rendered on the server for initial page loads or on the client for subsequent interactions and updates.

    Client Components are included in the client-side JavaScript bundle, which means they can increase the size of the bundle that needs to be downloaded, parsed, and executed on the client.

    They can fetch data from the server and update the UI in response to user interactions. They can also use effects, lifecycle methods, and other features of React.

## 2 Worlds (client/server)
  <a name="2-worlds"></a><a name="5.1"></a>
  - [5.1](#2-worlds) 2 Worlds (client/server)

## Sharing data client/server
  <a name="sharing-data"></a><a name="5.1"></a>
  - [5.1](#sharing-data) Sharing data client/server
