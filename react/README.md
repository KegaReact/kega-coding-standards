# React

## Table of Contents
  1. [Basic rules](#basic-rules)
  1. [Component structure](#component-structure)
  1. [Props](#props)
  1. [Alignment](#alignment)
  1. [Quotes](#quotes)
  1. [Spacing](#spacing)
  1. [CSS](#CSS)
   
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

## Props
  <a name="naming"></a><a name="1.1"></a>
  - [1.1](#naming) Use soft tabs (space character) set to 4 spaces. eslint: [`indent`](https://eslint.org/docs/rules/indent)
   
    ```javascript

    ```

## Alignment
  <a name="alignment"></a><a name="1.1"></a>
  - [1.1](#alignment) Alignment
   
    ```javascript

    ```

## Quotes
  <a name="quotes"></a><a name="1.1"></a>
  - [1.1](#quotes) Quotes
   
    ```javascript

    ```

## Spacing
  <a name="spacing"></a><a name="1.1"></a>
  - [1.1](#spacing) Spacing
   
    ```javascript

    ```

## CSS
  <a name="css-inline"></a><a name="1.1"></a>
  - [1.1](#css-inline) Inline styles
   
    ```javascript

    ```
  <a name="css-modules"></a><a name="1.1"></a>
  - [1.1](#css-modules) CSS Modules
   
    ```javascript

    ```
## Choices
- CSS Modules
- No typescript

