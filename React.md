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
- useEffect expects code inside it to be clear and synchronious , so writing asyncronous code will have to be wrapped with async/await , can't call it directly with try and catch method need to be wrapped in method
- React code splitting by using React.lazy to load a component asynchronously and <Suspense> to display a fallback "Loading..." UI while it fetches.
- ```
  const LazyComponent = React.lazy(() => import('./HeavyComponent'));
  --
  {/* Suspense catches the 'promise' from React.lazy */}
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
  ```
- On performance
  - use react's built in optimizations with React.memo , Pure componenets etc
  - Optimise state management -> avoid fr3equest rerender, state uplifting, can use redux
  - lazyLoading
  - use keys for listing data
  - used react virtualize for long list of data
- React Router DOM: import BrowserRouter as provider and <Routes> -> <Route path='pathName' element={<componentName>}> -usuage: <Link to="">text</Link>
  - use NavLink it adds active class , which we can used to set css for active elements
- 
- 
  -  
