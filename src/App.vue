/* eslint-disable vue/no-unused-components */
<template>
  <div id="app">
    <todo-app></todo-app>
  </div>
  
</template>

<script>
import ToDoApp from './components/ToDoApp.vue'

export default {
  name: 'App',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    ToDoApp
  }
}
</script>

