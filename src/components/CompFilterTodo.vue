<script setup>

</script>

<template>
  <h3>Filter Todo:</h3>
  <div class="filter-todo-box">
    <p>Filter By Status:</p>
    <div class="filter-complete">
      <div class="filter-item-box">
        <input type="radio" id="all" value="all" name="complete" v-on:change="onCompleteChange" checked>
        <label for="all">All</label>
      </div>
      <div class="filter-item-box">
        <input type="radio" id="completed" value="completed" name="complete" v-on:change="onCompleteChange">
        <label for="completed">Completed</label>
      </div>
      <div class="filter-item-box">
        <input type="radio" id="todo" value="todo" name="complete" v-on:change="onCompleteChange">
        <label for="todo">To do</label>
      </div>
    </div>
    <p>Filter By Priority:</p>
    <div class="filter-priority">
      <div class="filter-item-priority">
        <input type="checkbox" id="high" value="High" v-on:change="onPriorityChange">
        <label for="high">High</label>
      </div>
      <div class="filter-item-priority">
        <input type="checkbox" id="medium" value="Medium" v-on:change="onPriorityChange">
        <label for="medium">Medium</label>
      </div>
      <div class="filter-item-priority">
        <input type="checkbox" id="low" value="Low" v-on:change="onPriorityChange">
        <label for="low">Low</label>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'filter-todo',
  emits: ['changeCompletedFilter', 'changePriority'],
  props: {
    completedFilter: String,
    priorities: Array
  },
  data() {
    return {
      prioritiesSelected: []
    }
  },
  methods: {
    onCompleteChange(e) {
      const {value} = e.target
      this.$emit('changeCompletedFilter', value)
    },
    onPriorityChange(e) {
      const {checked, value} = e.target
      const data = {value, checked}
      this.$emit('changePriority', data)
    }
  }
}

</script>

<style scoped>

.filter-todo-box {

}

.filter-complete {
  display: flex;
  gap: 20px;
}

.filter-item-box {
  display: flex;
  gap: 10px;
}

.filter-item-box input {
  accent-color: #42b37a;
}

label {
  user-select: none;
}

.filter-priority {
  display: flex;
  gap: 30px;
}

.filter-item-priority {
  display: flex;
  gap: 10px;
}

.filter-item-priority input {
  accent-color: #42b37a;
}

p {
  margin-block: 10px;
}

</style>