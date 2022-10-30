<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from './components/HelloWorld.vue';
import { ref } from 'vue';

// A "ref" is a reactive data source that stores a value.
// Technically, we don't need to wrap the string with ref()
// in order to display it, but we will see in the next
// example why it is needed if we ever intend to change
// the value.
const message = ref('PaperLibrary');
</script>

<template>
  <div>
    <h1 class="paperlibrary">J-DU</h1>
    <h1>{{ message }}</h1>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.paperlibrary {
  background-color: Green;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
