<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos</h1>
      <input type="text" class="new-todo" placeholder="add a todo" v-model="newTodo" @keyup.enter="addTodo">
    </header>
    <div class="main">
      <ul class="todo-list">
        <li class="todo" :class="{completed: todo.completed}"  v-for="todo in todos" :key="todos.indexOf(todo)">
          <div class="view">
              <input type="checkbox" v-model="todo.completed" class="toggle">
              <label>{{ todo.name }}</label>
          </div>
        </li>
      </ul>
    </div>
    <footer class="footer">
      <span class="todo-count"><strong>{{ remaing }}</strong> items left</span>
      <ul class="filters">
        <li><a href="#" :class="{selected: filter == 'all'}" @click="filter = 'all'">All</a></li>
        <li><a href="#" :class="{selected: filter == 'todo'}" @click="filter = 'todo'">Active</a></li>
        <li><a href="#" :class="{selected: filter == 'done'}" @click="filter = 'done'">Completed</a></li>
      </ul>
    </footer>
  </section>
</template>

<script>
export default {
  data () {
    return {
      todos: [],
      newTodo: '',
      filter: 'all'
    }
  },

  methods: {
    addTodo () {
      this.todos.push({
        completed: false,
        name: this.newTodo
      })

      this.newTodo = ''
    }
  },

  computed: {
    remaing () {
      return this.todos.filter(todo => !todo.completed).length
    }
  }
}
</script>

<style src="./todos.css"></style>
