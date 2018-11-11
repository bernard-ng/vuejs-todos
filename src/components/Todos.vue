<template>
    <section class="todoapp">
        <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="add a todo" v-model="newTodo" @keydown.enter="addTodo">
        </header>
        <div class="main">
            <ul class="todo-list" v-for="todo in todos" :key='todo'>
                <li class="todo">
                    <div class="view">
                        <label>{{ todo }}</label>
                    </div>
                </li>
            </ul>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            todos: [],
            newTodo: '',
        }
    },

    methods: {
        addTodo() {
            this.todos.push(this.newTodo)
            this.newTodo = ''
        }
    }
}
</script>

<style src="./todos.css"></style>
