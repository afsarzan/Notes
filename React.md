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
  - soulution to stale closures
  - Get direct references of DOM element
