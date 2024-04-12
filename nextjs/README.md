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
    Nextjs has preserved namse for specific files like layout.js, page.js, error.js , ...
    
    ```
    // bad
    .
    ├── ...
    ├── app
    │   └── [storeCode]
            └── account
                ├── details
                ├── Navigation.moduel.css
                ├── layout.js
                ├── page.js
                └── OverviewPage.module.css
    
    └── ...

    // good
    .
    ├── ...
    ├── app
    │   └── [storeCode]
            └── account
                ├── details
                ├── layout.moduel.css
                ├── layout.js
                ├── page.js
                └── page.module.css
    
    └── ...
    ```

## Server component
  <a name="server-component"></a><a name="3.1"></a>
  - [3.1](#server-component) Server component
  - 
## Client component
  <a name="client-component"></a><a name="4.1"></a>
  - [4.1](#client-component) Client component

## 2 Worlds (client/server)
  <a name="2-worlds"></a><a name="5.1"></a>
  - [5.1](#2-worlds) 2 Worlds (client/server)

## Sharing data client/server
  <a name="sharing-data"></a><a name="5.1"></a>
  - [5.1](#sharing-data) Sharing data client/server
