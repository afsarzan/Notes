## Vue js
- 3 sections -> script, template and styled(scoped)
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
