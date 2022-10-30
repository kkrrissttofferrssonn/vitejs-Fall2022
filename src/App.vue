<script setup>
import { ref } from 'vue';
import TreeItem from './TreeItem.vue';
import HelloWorld from './components/HelloWorld.vue';
import PolyGraph from './PolyGraph.vue'
import { ref, reactive } from 'vue'

const newLabel = ref('')
const stats = reactive([
  { label: 'A', value: 100 },
  { label: 'B', value: 100 },
  { label: 'C', value: 100 },
  { label: 'D', value: 100 },
  { label: 'E', value: 100 },
  { label: 'F', value: 100 }
])

function add(e) {
  e.preventDefault()
  if (!newLabel.value) return
  stats.push({
    label: newLabel.value,
    value: 100
  })
  newLabel.value = ''
}

function remove(stat) {
  if (stats.length > 3) {
    stats.splice(stats.indexOf(stat), 1)
  } else {
    alert("Can't delete more!")
  }
}
const treeData = ref({
  name: 'My Tree',
  children: [
    { name: 'hello' },
    { name: 'world' },
    {
      name: 'child folder',
      children: [
        {
          name: 'child folder',
          children: [{ name: 'hello' }, { name: 'world' }],
        },
        { name: 'hello' },
        { name: 'world' },
        {
          name: 'child folder',
          children: [{ name: 'hello' }, { name: 'world' }],
        },
      ],
    },
  ],
});

const message = ref('PaperLibrary');
</script>

<template>
  <ul>
    <TreeItem class="item" :model="treeData"></TreeItem>
  </ul>
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
