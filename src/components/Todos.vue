<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos</h1>
      <input type="text" class="new-todo" placeholder="add a todo" v-model="newTodo" @keyup.enter="addTodo">
    </header>
    <div class="main">
      <input type="checkbox" class="toggle-all" v-model="allDone">
      <ul class="todo-list">
        <li class="todo" :class="{completed: todo.completed}"  v-for="todo in filteredTodos" :key="filteredTodos.indexOf(todo)">
          <div class="view">
              <input type="checkbox" v-model="todo.completed" class="toggle">
              <label>{{ todo.name }}</label>
              <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
          </div>
        </li>
      </ul>
    </div>
    <footer class="footer">
      <span class="todo-count"><strong>{{ remaing }}</strong> items left</span>
      <ul class="filters">
        <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">All</a></li>
        <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">Active</a></li>
        <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Completed</a></li>
      </ul>
    </footer>
  </section>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: "",
      filter: "all"
    }
  },

  methods: {
    addTodo() {
      this.todos.push({
        completed: false,
        name: this.newTodo
      })

      this.newTodo = ""
    },

    deleteTodo(todo) {
    }
  },

  computed: {
    remaing() {
      return this.filteredTodos.length
    },

    filteredTodos() {
      if (this.filter === "todo") {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === "done") {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    },

    allDone: {
      get() {
        return this.remaing === 0
      },

      set(value) {
        this.todos.forEach(todo => {
            todo.completed = value
          })
      }
    }
  }
}
</script>

<style src="./todos.css"></style>
