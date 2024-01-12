<script setup>

import CompTodoSearch from "@/components/CompTodoSearch.vue";
import CompAddTodo from "@/components/CompAddTodo.vue";
import CompTodoList from "@/components/CompTodoList.vue";
import CompFilterTodo from '@/components/CompFilterTodo.vue'

</script>

<template>
  <div class="todo-app">
    <comp-todo-search v-on:searchTodo="searchTodo"/>
    <comp-filter-todo
        v-bind:completedFilter="completedFilter"
        v-bind:priorities="priorities"
        v-on:change-completed-filter="changeCompleteFilter"
        v-on:change-priority="changePriority"
    />
    <comp-todo-list
        v-bind:todos="filteredTodos"
        v-bind:search="search"
        v-on:toggle-completed="toggleCompleted"
        v-on:delete-todo="deleteTodo"
    />
    <comp-add-todo v-on:addTodo="addTodo"/>
  </div>
</template>

<script>

export default {
  name: 'todo-app',
  data() {
    return {
      todos: this.bindTodos() ?? [],
      search: '',
      filteredTodos: this.bindTodos() ?? [],
      completedFilter: 'all',
      priorities: []
    }
  },
  methods: {
    addTodo(data) {
      const newTodo = {id: Date.now(), content: data.task, completed: false, priority: data.priority}
      this.todos = [...this.todos, newTodo]
      this.filteredTodos = this.filterTodos(this.search)
      this.bindTodos(this.todos)
    },
    bindTodos(todosArg) {
      if (todosArg) localStorage.setItem('todos', JSON.stringify(todosArg))
      else return JSON.parse(localStorage.getItem('todos'))
    },
    searchTodo(data) {
      const {search} = data
      this.search = search
      console.log(data)
      this.filteredTodos = this.filterTodos(search)
    },
    filterTodos(filter) {
      return [...this.todos].filter(todo => {
        if (this.completedFilter === 'all') {
          return todo.content.toLowerCase().includes(filter.toLowerCase()) &&
              (this.priorities.length ? this.priorities.includes(todo.priority) : true)
        }

        return todo.content.toLowerCase().includes(filter.toLowerCase()) &&
            (this.completedFilter === 'completed' ? todo.completed : !todo.completed) &&
            (this.priorities.length ? this.priorities.includes(todo.priority) : true)
      })
    },
    changeCompleteFilter(completeOption) {
      this.completedFilter = completeOption
      this.filteredTodos = this.filterTodos(this.search)
    },
    changePriority({value, checked}) {
      if (checked) {
        this.priorities = [...this.priorities, value]
      }
      else {
        this.priorities = [...this.priorities].filter(priority => priority !== value)
      }
      this.filteredTodos = this.filterTodos(this.search)
    },
    toggleCompleted(_id) {
      this.todos = [...this.todos].map(todo => ({
        ...todo,
        completed: todo.id === _id ? !todo.completed : todo.completed
      }))
      this.filteredTodos = this.filterTodos(this.search)
      this.bindTodos(this.todos)
    },
    deleteTodo(_id) {
      this.todos = [...this.todos].filter(todo => todo.id !== _id)
      this.filteredTodos = this.filterTodos(this.search)
      this.bindTodos(this.todos)
    }
  },
  computed: {},
}

</script>

<style scoped>
.todo-title {
  text-align: center;
}

.todo-app {
  max-width: 600px;
  height: 90vh;
  overflow-y: auto;
  width: 100%;
  padding: 20px;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  box-shadow: 0 10px 15px #ccc;
}
</style>