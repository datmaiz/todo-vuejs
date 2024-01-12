<script setup>

</script>

<template>
  <h3>Add New Todo:</h3>
  <div class="todo-add-box">
    <input type="text" placeholder="Enter new task" autofocus class="todo-add-input" v-model="task" v-on:keydown="handleKeyDown">
    <select v-model="priority" class="priority" :class="priority.toLowerCase()">
      <option value="High" class="priority high">High</option>
      <option value="Medium" class="priority medium">Medium</option>
      <option value="Low" class="priority low">Low</option>
    </select>
    <button type="button" class="add-task-btn" v-on:click="addTodo">Add task</button>
  </div>
</template>

<script>

export default {
  name: 'todo-add',
  emits: ['addTodo'],
  data() {
    return {
      task: '',
      priority: 'Medium',
    }
  },
  methods: {
    addTodo() {
      const data = {task: this.task, priority: this.priority}
      this.task = ''
      this.priority = 'Medium'
      this.$emit('addTodo', data)
    },
    handleKeyDown(e) {
      const {keyCode} = e
      if (keyCode === 13) this.addTodo()
    }
  }
}

</script>

<style scoped>

.todo-add-box {
  display: flex;
  justify-content: space-between;
}

.todo-add-input {
  flex: 1;
  padding: 10px 15px;
  outline: none;
  border: 1px solid #ccc;
}

.add-task-btn {
  padding: 6px 18px;
  background-color: #42b37a;
  font-weight: 500;
  outline: none;
  border: 1px solid #42b37a;
  color: #fff;
}

.priority {
  cursor: pointer;
  outline: none;
}

</style>