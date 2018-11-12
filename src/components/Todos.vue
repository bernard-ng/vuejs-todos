<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos</h1>
      <input type="text" class="new-todo" placeholder="add a todo" v-model="newTodo" @keyup.enter="addTodo">
    </header>
    <div class="main">
      <input type="checkbox" class="toggle-all" v-model="allDone">
      <ul class="todo-list">
        <li class="todo" :class="{completed: todo.completed, editing: todo === editing}"  v-for="todo in filteredTodos" :key="filteredTodos.indexOf(todo)">
          <div class="view">
              <input type="checkbox" v-model="todo.completed" class="toggle">
              <label @dblclick="editTodo(todo)">{{ todo.name }}</label>
              <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
          </div>
          <input type="text" class="edit" v-model="todo.name">
        </li>
      </ul>
    </div>
    <footer class="footer" v-show="hasTodos">
      <span class="todo-count"><strong>{{ remaing }}</strong> items left</span>
      <ul class="filters">
        <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">All</a></li>
        <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">Active</a></li>
        <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Completed</a></li>
      </ul>
      <button class="clear-completed" v-if="completed" @click="deleteCompleted">Delete completed items</button>
    </footer>
  </section>
</template>

<script>
export default {
  data () {
    return {
      todos: [],
      newTodo: '',
      editing: null,
      filter: 'all'
    }
  },

  methods: {
    addTodo () {
      this.todos.push({
        completed: false,
        name: this.newTodo
      })

      this.newTodo = ""
    },

    deleteTodo (todo) {
      this.todos = this.todos.filter(i => i !== todo)
    },

    editTodo (todo) {
      this.editing = todo
    },

    doneEdit () {
      this.editing = null
    },

    deleteCompleted () {
      this.todos = this.todos.filter(todo => !todo.completed)
    }
  },

  computed: {
    remaing () {
      return this.todos.filter(todo => !todo.completed).length
    },

    completed () {
      return this.todos.filter(todo => !todo.completed)
    },

    filteredTodos () {
      if (this.filter === 'todo') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === 'done') {
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
    },

    hasTodos () {
      return this.todos.length > 0
    }
  }
}
</script>

<style src="./todos.css"></style>
