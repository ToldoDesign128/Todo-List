<script setup>
import TodoInput from './components/TodoInput.vue';
</script>

<template>
  <TodoInput/>
</template>

<style lang="scss">

  body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    background: linear-gradient(to bottom right, #99C191, #C3D98D);
  }
  #app {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 1rem;
    color: #333;
    width: 100%;
    max-width: 768px;
  }

</style>