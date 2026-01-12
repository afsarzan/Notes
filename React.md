# React nuances

- ```useRef``` :  Applications 
  - usesRef Callback, replacing useLayoutEffect
  -   Called with elements on mount and runs synchronoously before paint, no need to check references below code will run on order
  -   ```
        const divRef = (div) => {
          div.style.backgroundColor =  'red';
        }

        ---

          return <div ref={divRef} id="content">
                  ...
                  </div>
      ```
  - DOM list references
  - Storage
      -   able to store any type of value  
  - soulution to stale closures
  - Get direct references of DOM element
---
- **Life Cycle phases**
 1) Mounting 2) Updating 3) Unmounting 4) Error Handling
 2)  On class based components
   - On Mounting
     - Constructor
     - getDerivedStateFromProps
     - Render
     - ComponentDidMount
   - On Update
     - GetDerivedStateFromProps
     - shouldComponentUpdate
     - render
     - getSnapshotBeforeUpdate
     - componentDidUpdate
- on unmount
     - componentWillunmount
- ErrorBoundaryies
  -   getDerivedStateFromProps and componentDidCatch is used for managing error
---
-
