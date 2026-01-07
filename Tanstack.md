**Tanstack start v0 nuances**
- To begin use -> npm create @tanstack/start@latest
- Route.useLoaderDat -> to fetch data from loader or from async call
- createServerFn is used to tell code to run on server it accepts methods and chained to handler function
- <Button asChild -> why use asChild in shadcn -> The Button's styles and props are applied to the Link, but only the Link is rendered.
- CreateIsoMorphicFn().server().client() -> can be used customly
- **example**: 
  - ``` createIsomorphicFn.server( () => { // Server-only code here }).client( () => {// Client-only code here }) ```
