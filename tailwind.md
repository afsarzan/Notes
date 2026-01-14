### Tailwind Nuances
---

- To change text use text-{xl,2xl,bold,etc}, font-{bold,semibold}
-  ##  Layout & Display
  ```
   .block                -> display: block;
  .inline               -> display: inline;
  .inline-block         -> display: inline-block;
  .flex                 -> display: flex;
  .inline-flex          -> display: inline-flex;
  .grid                 -> display: grid;
  .hidden               -> display: none;
  
  .visible              -> visibility: visible;
  .invisible            -> visibility: hidden;
  
  .overflow-hidden      -> overflow: hidden;
  .overflow-auto        -> overflow: auto;
  .overflow-scroll      -> overflow: scroll;
  .overflow-x-auto      -> overflow-x: auto;
  .overflow-y-auto      -> overflow-y: auto;
  ```
- ## Positioning
 ```
.static               -> position: static;
.relative             -> position: relative;
.absolute             -> position: absolute;
.fixed                -> position: fixed;
.sticky               -> position: sticky;

.inset-0              -> top: 0; right: 0; bottom: 0; left: 0;
.inset-x-0            -> left: 0; right: 0;
.inset-y-0            -> top: 0; bottom: 0;
.top-0                -> top: 0;
.right-0              -> right: 0;
.bottom-0             -> bottom: 0;
.left-0               -> left: 0;

/* Common offsets (Tailwind spacing scale) */
.top-1                -> top: 0.25rem;        /* 4px */
.top-2                -> top: 0.5rem;         /* 8px */
.top-4                -> top: 1rem;           /* 16px */
.top-8                -> top: 2rem;           /* 32px */

.z-0                  -> z-index: 0;
.z-10                 -> z-index: 10;
.z-20                 -> z-index: 20;
.z-30                 -> z-index: 30;
.z-40                 -> z-index: 40;
.z-50                 -> z-index: 50;
.z-auto               -> z-index: auto;
``
