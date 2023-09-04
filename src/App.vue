<template>
  <div>
    <h1>Item List</h1>
    <ul v-if="items.length">
      <li v-for="(item, index) in items" :key="index">{{ item }}</li>
    </ul>
    <p v-else>No items available.</p>
    <input type="text" v-model="newItem" />
    <button @click="addItem">Add Item</button>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from "vue";

// Measure the time just before the component is added to the DOM
const preRenderTime = performance.now();

const items = ref(["Item 1", "Item 2"]);
const newItem = ref("");

const addItem = () => {
  // Record time before the DOM update
  const beforeUpdate = performance.now();

  // Perform the DOM update (i.e., add item to the list)
  items.value.push(newItem.value);

  // Force the component to re-render immediately and measure performance
  nextTick(() => {
    // Record time after the DOM update
    const afterUpdate = performance.now();

    // Log the time taken to the console
    console.log(`Time taken to update DOM: ${afterUpdate - beforeUpdate} ms`);
  });

  // Reset the newItem input field
  newItem.value = "";
};

onMounted(() => {
  // Measure the time right after the component has been added to the DOM
  const postRenderTime = performance.now();
  console.log(`Component rendering time: ${postRenderTime - preRenderTime} ms`);
});
</script>

<style scoped>
div {
  text-align: center;
  margin-top: 2em;
}

h1 {
  font-size: 2em;
  margin-bottom: 1em;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 0.5em 0;
  padding: 0.5em;
  border: 1px solid #ccc;
  width: 200px;
  margin-left: auto;
  margin-right: auto;
}

input {
  margin-right: 1em;
  padding: 0.5em;
}

button {
  padding: 0.5em 1em;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}
</style>
