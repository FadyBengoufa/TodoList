<template>
  <div>
    <!--<img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <todos></todos>
  </div>
</template>

<script>
import todos from './components/Todos.vue'

export default {
  name: 'app',
  components: {
    todos
  }
}
</script>

<style src="./assets/css/style.css"></style>
