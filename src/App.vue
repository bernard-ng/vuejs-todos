<template>
  <div id="app">
    <Todos v-model="todos"/>
    <Todos v-model="todos"/>
    <Todos/>

    <button @click="addTodo">Add a somethink todo</button>
  </div>
</template>

<script>
import Todos from './components/Todos'

export default {
  name: 'app',

  data () {
    return {
      todos: [{
        name: 'demo',
        completed: true
      }]
    }
  },

  methods: {
    addTodo () {
      this.todos.push({
        name: 'bernard ng',
        completed: false
      })
    }
  },

  components: {
    Todos
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
