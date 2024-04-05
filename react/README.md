# React

## Table of Contents
  1. [Basic rules](#basic-rules)
  1. [Component structure](#component-structure)
  1. [Props](#props)
  1. [Alignment](#alignment)
  1. [Quotes](#quotes)
  1. [Spacing](#spacing)
  1. [CSS](#css)
  1. [Hook dependencies](#hook-dependencies)
   
## Basic rules
  <a name="basic-rules"></a><a name="1.1"></a>
  - Only include one React component per file.


## Component structure
  <a name="component-structure"></a><a name="1.1"></a>
  - [1.1](#component-structure) Basic structure of a react component
   
    ```javascript
    const Component = () => {
        // Hooks
        const dispatch = useDispatch();
        const value = useValue();
    
        const { data } = useData();
        const { otherData } = useOtherData();

        const [ state, setState ] = useState();

        // Effects
        useEffect(() => {}, []);
        useMemo(() => {}, []);

        // Callback functions
        const onClick = () => {
        }
      
        return (
            <div>
                <h1>Component<h1/>
                <button onClick={onClick}>Button</button>
            </div>
        );
    }

    export default Component;
    ```
     > Try to keep the component readable, keep the variables & functions in the structure as shown above. Sort the hooks on return types value, {}, [] then effects like useEffect and callbacks. This way other developers know where to look when they need to work in youre code.

 <a name="component-import-structure"></a><a name="1.2"></a>
 - [1.2](#component-import-structure) Basic import structure
   ```javascript
   // React imports
   import { useState, useMemo, useEffect } from 'react';

   // 3 party imports
   import classNames from 'classnames';

   // Own componets import
   import { Button } from '@/components/button';
   import { Col, Row, Container } from '@/components/grid';

   import useData from '@/hooks/useData';
   import useOtherData from '@/hooks/useOtherData';

   // Style import
   import classes from './Component.module.css';
   
   const Component = () => {
        ...
   }
   ```
   > Try to keep the import in the structure as shown above. Sort the imports on imported types value, {}, useHook and imports from specific direcories like lib of modules or functions. This keeps the component file readable for other developers.

## Props
  <a name="props"></a><a name="2.1"></a>
  - [2.1](#props) Naming props for Components

    Use camelCase for prop names for functions and hooks, or PascalCase for Components

    ```javascript 
     // bad
     const Component = ({ variabe_name, component }) => { }

     // good
     const Component = ({ variabeName, Component }) => { }
    ```
  <a name="props-fallback"></a><a name="2.2"></a>
  - [2.2](#props-fallback) Use fallback values if pros are optional or the value never should be undefined.

    ```javascript 
     // bad
     const Component = ({ name, optional }) => { }

     // good
     const Component = ({ name, optional=false }) => { }
    ```
    > If the prop isn't set it will be undefined this can cause problems.
## Alignment
  <a name="alignment"></a><a name="3.1"></a>
  - [3.1](#alignment) Alignment 
   
    ```javascript
     // bad
     <Component props1="has a value" props2="has an other value" props3="has an other value" props4="has more value" props5="has more value" />

     // good
     <Component
         props1="has a value"
         props2="has an other value"
         props3="has an other value"
         props4="has more value" props5="has more value"
     />
    ```
    > Try to align youre code so it is easy to read on every type of screen.
    
## Quotes
  <a name="quotes"></a><a name="4.1"></a>
  - [4.1](#quotes) Quotes, use double quotes (") for JSX attributes, but single quotes (') for all other JS.

    > Why? Regular HTML attributes also typically use double quotes instead of single, so JSX attributes mirror this convention.

    ```javascript
    // bad
    <Component bar='bar' />
    
    // good
    <Component bar="bar" />
    
    // bad
    <Component style={{ left: "20px" }} />
    
    // good
    <Component style={{ left: '20px' }} />
    ```
    
## Spacing
  <a name="spacing"></a><a name="5.1"></a>
  - [5.1](#spacing) Spacing
   
    ```javascript
    // bad
    <Component style={{left:'20px'}} />
    <Component style={ {left:'20px'} } />
    
    const Component = ( { name, optional = false } ) => { }

    // good
    <Component style={{ left: '20px' }} />
    
    const Component = ({ name, optional=false }) => { }
    ```

    > Try to space your props as shown above. all code bases have consistent readable code.
    
## CSS
  <a name="css"></a><a name="6.1"></a>
  - [6.1](#css) Inline styles
   
    ```javascript

    ```
  <a name="css-modules"></a><a name="6.2"></a>
  - [6.2](#css-modules) CSS Modules
   
    ```javascript

    ```
## Hook dependencie
  <a name="hook-dependencies"></a><a name="7.1"></a>
  - [7.1](#hook-dependencies) Hook dependencies
   
    ```javascript
    // bad
    
    const obj = { test: 'test' }
    obj.test = 'test1';
  
    useEffect(() => {}, [ obj ]); // Will not trigger

    const arr = [ 0, 1, 2 ];
    arr.push(3);
    
    useEffect(() => {}, [ arr ]); // Will not trigger

    // good
    
    let obj = { test: 'test' }
    obj.test = 'test1';

    useEffect(() => {}, [ obj.test ]); // Will trigger

    or
    
    obj = {
      ...obj,
      test: 'test1'
    }
    
    useEffect(() => {}, [ obj ]); // Will trigger

    let arr = [ 0, 1, 2 ];
    arr = [ ...arr, 3 ];
    
    useEffect(() => {}, [ arr ]); // Will trigger

    ```
    > React compares the values in the dependency array when there is a change the hook wil trigger but for objects or array only the reference is checked not the content of an object or array. So make shure an array or object is cloned.
     
## Choices
- CSS Modules
- No typescript

