<script setup>

</script>

<template>
  <h3>Search Todo:</h3>
  <div class="todo-search-box">
    <input type="text" placeholder="Search task" class="todo-search-input" v-model="search" v-on:keydown="handleKeyDown">
    <button type="button" class="search-task-btn" v-on:click="searchTodo">Search</button>
  </div>
</template>


<script>

export default {
  name: 'todo-search',
  emits: ['searchTodo'],
  data() {
    return {
      search: ''
    }
  },
  methods: {
    searchTodo() {
      const data = {search: this.search}

      this.$emit('searchTodo', data)
    },
    handleKeyDown(e) {
      const {keyCode} = e
      if (keyCode === 13) this.searchTodo()
    }
  }
}

</script>

<style scoped>
  .todo-search-box {
    display: flex;
    justify-content: space-between;
  }

  .todo-search-input {
    flex: 1;
    padding: 10px 15px;
    outline: none;
    border: 1px solid #ccc;
  }

  .search-task-btn {
    padding: 6px 18px;
    background-color: #42b37a;
    font-weight: 500;
    outline: none;
    border: 1px solid #42b37a;
    color: #fff;
    transition: 0.25s linear;
  }

  .search-task-btn:hover {
    background-color: #fff;
    color: #333;
  }

  .search-task-btn:active {
    background-color: #42b37a;
    color: #fff;
  }
</style>