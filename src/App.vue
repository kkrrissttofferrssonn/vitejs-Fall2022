<script setup>
import { ref, reactive } from 'vue';
import { shuffle as _shuffle } from 'lodash-es';
import TreeItem from './TreeItem.vue';
import HelloWorld from './components/HelloWorld.vue';
import PolyGraph from './PolyGraph.vue';

const getInitialItems = () => [1, 2, 3, 4, 5];
const items = ref(getInitialItems());
let id = items.value.length + 1;

function insert() {
  const i = Math.round(Math.random() * items.value.length);
  items.value.splice(i, 0, id++);
}

function reset() {
  items.value = getInitialItems();
}

function shuffle() {
  items.value = _shuffle(items.value);
}

function remove(item) {
  const i = items.value.indexOf(item);
  if (i > -1) {
    items.value.splice(i, 1);
  }
}
const newLabel = ref('');
const stats = reactive([
  { label: 'A', value: 100 },
  { label: 'B', value: 100 },
  { label: 'C', value: 100 },
  { label: 'D', value: 100 },
  { label: 'E', value: 100 },
  { label: 'F', value: 100 },
]);

function add(e) {
  e.preventDefault();
  if (!newLabel.value) return;
  stats.push({
    label: newLabel.value,
    value: 100,
  });
  newLabel.value = '';
}

function remove(stat) {
  if (stats.length > 3) {
    stats.splice(stats.indexOf(stat), 1);
  } else {
    alert("Can't delete more!");
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
  <svg width="200" height="200">
    <PolyGraph :stats="stats"></PolyGraph>
  </svg>

  <!-- controls -->
  <div v-for="stat in stats">
    <label>{{ stat.label }}</label>
    <input type="range" v-model="stat.value" min="0" max="100" />
    <span>{{ stat.value }}</span>
    <button @click="remove(stat)" class="remove">X</button>
  </div>

  <form id="add">
    <input name="newlabel" v-model="newLabel" />
    <button @click="add">Add a Stat</button>
  </form>

  <pre id="raw">{{ stats }}</pre>
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
  <button @click="insert">insert at random index</button>
  <button @click="reset">reset</button>
  <button @click="shuffle">shuffle</button>

  <TransitionGroup tag="ul" name="fade" class="container">
    <div v-for="item in items" class="item" :key="item">
      {{ item }}
      <button @click="remove(item)">x</button>
    </div>
  </TransitionGroup>
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
<style>
polygon {
  fill: DarkOrange;
  opacity: 0.75;
}

circle {
  fill: transparent;
  stroke: #999;
}

text {
  font-size: 10px;
  fill: #666;
}

label {
  display: inline-block;
  margin-left: 10px;
  width: 20px;
}

#raw {
  position: absolute;
  top: 0;
  left: 300px;
}
.item {
  cursor: pointer;
  line-height: 1.5;
}
.bold {
  font-weight: bold;
}
container {
  position: relative;
  padding: 0;
}

.item {
  width: 100%;
  height: 30px;
  background-color: #f3f3f3;
  border: 1px solid #666;
  box-sizing: border-box;
}

/* 1. declare transition */
.fade-move,
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
}

/* 2. declare enter from and leave to state */
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: scaleY(0.01) translate(30px, 0);
}

/* 3. ensure leaving items are taken out of layout flow so that moving
      animations can be calculated correctly. */
.fade-leave-active {
  position: absolute;
}
</style>
