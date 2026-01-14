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
```
## Spacing (Margin & Padding)
```
/* Margin (all sides) */
.m-0                  -> margin: 0;
.m-px                 -> margin: 1px;
.m-4                  -> margin: 1rem;

/* Margin (axis) */
.mx-4                 -> margin-left: 1rem; margin-right: 1rem;
.my-2                 -> margin-top: 0.5rem; margin-bottom: 0.5rem;

/* Margin (sides) */
.mt-6                 -> margin-top: 1.5rem;
.mr-3                 -> margin-right: 0.75rem;
.mb-8                 -> margin-bottom: 2rem;
.ml-1.5               -> margin-left: 0.375rem;

/* Auto centering */
.mx-auto              -> margin-left: auto; margin-right: auto;

/* Negative margins */
.-mt-4                -> margin-top: -1rem;

/* Padding mirrors margin */
.p-4                  -> padding: 1rem;
.px-6                 -> padding-left: 1.5rem; padding-right: 1.5rem;
.py-2.5               -> padding-top: 0.625rem; padding-bottom: 0.625rem;
.pt-3                 -> padding-top: 0.75rem;
```
---
- ## Flexbox
```
.flex-row             -> flex-direction: row;
.flex-row-reverse     -> flex-direction: row-reverse;
.flex-col             -> flex-direction: column;
.flex-col-reverse     -> flex-direction: column-reverse;

.flex-wrap            -> flex-wrap: wrap;
.flex-nowrap          -> flex-wrap: nowrap;
.flex-wrap-reverse    -> flex-wrap: wrap-reverse;

.items-start          -> align-items: flex-start;
.items-center         -> align-items: center;
.items-end            -> align-items: flex-end;
.items-stretch        -> align-items: stretch;
.items-baseline       -> align-items: baseline;

.justify-start        -> justify-content: flex-start;
.justify-center       -> justify-content: center;
.justify-end          -> justify-content: flex-end;
.justify-between      -> justify-content: space-between;
.justify-around       -> justify-content: space-around;
.justify-evenly       -> justify-content: space-evenly;

.content-start        -> align-content: flex-start;
.content-center       -> align-content: center;
.content-end          -> align-content: flex-end;
.content-between      -> align-content: space-between;
.content-around       -> align-content: space-around;
.content-evenly       -> align-content: space-evenly;

.gap-0                -> gap: 0;
.gap-2                -> gap: 0.5rem;
.gap-4                -> gap: 1rem;
.gap-x-6              -> column-gap: 1.5rem;
.gap-y-3              -> row-gap: 0.75rem;

.self-auto            -> align-self: auto;
.self-start           -> align-self: flex-start;
.self-center          -> align-self: center;
.self-end             -> align-self: flex-end;
.self-stretch         -> align-self: stretch;

.flex-1               -> flex: 1 1 0%;
.flex-auto            -> flex: 1 1 auto;
.flex-initial         -> flex: 0 1 auto;
.flex-none            -> flex: none;

.grow                 -> flex-grow: 1;
.grow-0               -> flex-grow: 0;
.shrink               -> flex-shrink: 1;
.shrink-0             -> flex-shrink: 0;

.order-first          -> order: -9999;
.order-last           -> order: 9999;
.order-none           -> order: 0;
.order-1              -> order: 1;
```
---

##  Borders & Radius
```
.border               -> border-width: 1px;
.border-0             -> border-width: 0;
.border-2             -> border-width: 2px;
.border-4             -> border-width: 4px;
.border-t             -> border-top-width: 1px;
.border-x-2           -> border-left-width: 2px; border-right-width: 2px;

.border-solid         -> border-style: solid;
.border-dashed        -> border-style: dashed;
.border-dotted        -> border-style: dotted;

.border-gray-200      -> border-color: #e5e7eb;
.border-slate-700     -> border-color: #334155;
.border-blue-500      -> border-color: #3b82f6;

/* Radius */
.rounded-none         -> border-radius: 0;
.rounded-sm           -> border-radius: 0.125rem;
.rounded               -> border-radius: 0.25rem;
.rounded-md           -> border-radius: 0.375rem;
.rounded-lg           -> border-radius: 0.5rem;
.rounded-xl           -> border-radius: 0.75rem;
.rounded-2xl          -> border-radius: 1rem;
.rounded-3xl          -> border-radius: 1.5rem;
.rounded-full         -> border-radius: 9999px;
.rounded-t-lg         -> border-top-left-radius: 0.5rem; border-top-right-radius: 0.5rem;
```

