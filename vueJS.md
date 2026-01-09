## Vue js 
- 3 sections -> script, template and styled(scoped) - SFC(Single file compnent)
- Two APIs, options and composition
- directives  ```v-if, v-else, v-else-if, v-for with :key="uniqueId" ```
- v-bind:href or :href for binding anchor
- data() method in script return binding variables just like stage in react
- methods:{} -> here you can write methods used on events
  ```
  method: {
   toggleStatus () {
    ...
    }
  }
  ```
- v-on:click or @click= "toggleStatus" for clicking events
- #In composition API you should use setup() method to set states
- and should return explicitly each property and method and to make them reactive use ```ref``` imported from vue
- To make use of value better use .value property not this binding like in options API
-  You can also use ```<script setup>``` in script tag the can avoid writing setup method in script element
-  @submit on form is used to submit forms also we can use @submit.prevent to have prevent default implemented by default
-  v-model to bind ref to inputs, to access it use .value
-  ```vue-createApp()``` is used to bootstrap
-  ```
   defineProps({
     propertyName:{
       type: String/boolean, etc
       default: 'Default value'
   });```
- Above method in child component -> import { defineProps } from 'vue'
- Computed properties are used to handle complex logic that depends on reactive data
- ```
  <script setup>
      import { ref, computed } from 'vue';
      
      // Reactive data
      const firstName = ref('Jane');
      const lastName = ref('Doe');
      
      // Computed property
      const fullName = computed(() => {
        return `${firstName.value} ${lastName.value}`;
      });
      </script>
  ```
-  Vue uses offical Vue Router library for switching between pages
-  ```
   import { createRouter, createWebHistory } from 'vue-router';
    import Home from './Home.vue';
    import About from './About.vue';
    
    const routes = [
      { path: '/', component: Home },
      { path: '/about', component: About }
    ];
    
    const router = createRouter({
      history: createWebHistory(),
      routes,
    });
    
    export default router;
   ```
  - <router-link>: Creates a clickable link (replaces the standard <a> tag).
  - <router-view>: A placeholder where the current page component will be rendered.
  - To protect routes, we use meta property, Use router.beforeEach to check the requiresAuth tag before the navigation is finished.
  - ```
    const routes = [
      { 
        path: '/dashboard', 
        component: Dashboard, 
        // This custom property tells our guard to check for auth
        meta: { requiresAuth: true } 
      },
      { 
        path: '/login', 
        component: Login 
      }
    ];

    router.beforeEach((to, from) => {
        // 1. Check if the destination route needs authentication
        const isAuthRequired = to.matched.some(record => record.meta.requiresAuth);
        
        // 2. Check if the user is actually logged in (e.g., from a Pinia store or LocalStorage)
        const isAuthenticated = !!localStorage.getItem('user_token');
      
        // 3. Logic: If auth is required but user isn't logged in, redirect to login
        if (isAuthRequired && !isAuthenticated) {
          return { path: '/login' };
        }
        
        // If authorized or route is public, let them through
        return true; 
      });
    ```
- useRoute to get route path.
- to handle 404, use /:pathMatch(.*)*
- ```
   const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
  // ... other routes ...

  // The 404 Catch-all Route
  { 
    path: '/:pathMatch(.*)*', 
    name: 'NotFound', 
    component: () => import('./views/NotFound.vue') 
  }

  ]; ```
- onMounted() -> can be used to make axios calls to get data from server
- setup a proxy proery in defineconfig of vite to replace long path with '/api' path
- 
   
  
