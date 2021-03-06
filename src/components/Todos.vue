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
          <input type="text" class="edit" v-model="todo.name" v-focus="todo === editing" @keyup.enter="doneEdit" @blur="doneEdit" @keyup.esc="cancelEdit">
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
import Vue from 'vue'

export default {
  props: {
    value: {type: Array, default () { return [] }}
  },

  data () {
    return {
      todos: this.value,
      newTodo: '',
      oldTodo: '',
      editing: null,
      filter: 'all'
    }
  },

  watch: {
    value (value) {
      this.todos = value
    }
  },

  methods: {
    addTodo () {
      this.todos.push({
        completed: false,
        name: this.newTodo
      })

      this.newTodo = ''
      this.$emit('input', this.todos)
    },

    deleteTodo (todo) {
      this.todos = this.todos.filter(i => i !== todo)
      this.$emit('input', this.todos)
    },

    editTodo (todo) {
      this.editing = todo
      this.oldTodo = todo.name
    },

    doneEdit () {
      this.editing = null
    },

    cancelEdit () {
      this.editing.name = this.oldTodo
      this.doneEdit()
    },

    deleteCompleted () {
      this.todos = this.todos.filter(todo => !todo.completed)
      this.$emit('input', this.todos)
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
      get () {
        return this.remaing === 0
      },

      set (value) {
        this.todos.forEach(todo => {
          todo.completed = value
        })
      }
    },

    hasTodos () {
      return this.todos.length > 0
    }
  },

  directives: {
    focus (el, value) {
      if (value) {
        Vue.nextTick(() => {
          el.focus()
        })
      }
    }
  }
}
</script>

<style src="./todos.css"></style>
