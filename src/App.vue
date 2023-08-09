<script setup lang="ts">
import { RouterView } from 'vue-router'
import TodoHeader from './components/TodoHeader.vue'
</script>

<template>
  <!-- template approach was added just to use it once in the project (would not be necessary since there are no reusable components) -->
  <TodoHeader>
    <template #app-name>ToDos</template>
  </TodoHeader>
  <RouterView />
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;500;600;700&display=swap');

* {
  font-family: "Rubik", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 1rem;
}
</style>