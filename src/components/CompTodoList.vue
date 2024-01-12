<script setup>

</script>

<template>
  <h3>List Todo: </h3>
  <div class="todo-list">
    <ul class="todos" v-if="todos.length">
      <li class="todo" v-for="todo in todos" v-bind:key="todo.id">
        <input type="checkbox" v-bind:checked="todo.completed" class="todo-completed" :id="todo.id"
               v-on:change="toggleCompleted(todo.id)">
        <svg height="32" id="Layer_1" viewBox="0 0 32 32" width="32"
             v-on:click="deleteTodo(todo.id)"
             xml:space="preserve" xmlns="http://www.w3.org/2000/svg">
          <g>
            <polyline fill="none" points="649,137.999 675,137.999 675,155.999 661,155.999" stroke="#FFFFFF"
                      stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="2"/>
            <polyline fill="none" points="653,155.999 649,155.999 649,141.999" stroke="#FFFFFF" stroke-linecap="round"
                      stroke-linejoin="round" stroke-miterlimit="10" stroke-width="2"/>
            <polyline fill="none" points="661,156 653,162 653,156" stroke="#FFFFFF" stroke-linecap="round"
                      stroke-linejoin="round" stroke-miterlimit="10" stroke-width="2"/>
          </g>
          <g>
            <path
                d="M11.312,12.766c0.194,0.195,0.449,0.292,0.704,0.292c0.255,0,0.51-0.097,0.704-0.292c0.389-0.389,0.389-1.02,0-1.409 L4.755,3.384c-0.389-0.389-1.019-0.389-1.408,0s-0.389,1.02,0,1.409L11.312,12.766z"/>
            <path
                d="M17.407,16.048L28.652,4.793c0.389-0.389,0.389-1.02,0-1.409c-0.389-0.389-1.019-0.561-1.408-0.171L15.296,15 c0,0-0.296,0-0.296,0s0,0.345,0,0.345L3.2,27.303c-0.389,0.389-0.315,1.02,0.073,1.409c0.194,0.195,0.486,0.292,0.741,0.292 s0.528-0.097,0.722-0.292L15.99,17.458l11.249,11.255c0.194,0.195,0.452,0.292,0.706,0.292s0.511-0.097,0.705-0.292   c0.389-0.389,0.39-1.02,0.001-1.409L17.407,16.048z"/>
          </g>
        </svg>
        <label :for="todo.id" class="todo-content">{{ todo.content }}</label>
        <span class="todo-priority" :class="todo.priority.toLowerCase()">{{ todo.priority }}</span>
      </li>
    </ul>
    <ul class="message todos" v-else>No Todo</ul>
  </div>
</template>

<script>

export default {
  name: 'todo-list',
  emits: ['toggleCompleted', 'deleteTodo'],
  props: {
    todos: Array,
    search: String,
  },
  data() {
    return {}
  },
  methods: {
    toggleCompleted(_id) {
      this.$emit('toggleCompleted', _id)
    },
    deleteTodo(_id) {
      this.$emit('deleteTodo', _id)
    }
  },
  computed: {}
}

</script>

<style scoped>
.todo-list {
  flex: 1;
  padding: 20px 10px;
  border: 1px solid #ccc;
  overflow-y: auto;
}

::-webkit-scrollbar {
  width: 5px;
  height: 5px;
}

::-webkit-scrollbar-thumb {
  background-color: #42b37a;
}

.todo {
  display: flex;
  align-items: center;
  gap: 5px;
  padding-left: 10px;
  margin-top: 10px;
  transition: 0.25s;
  cursor: pointer;
}

.todo:hover {
  background-color: rgba(204, 204, 204, 0.17);
}

.todo-completed {
  zoom: 1.3;
  accent-color: #42b37a;
  cursor: pointer;
  border-radius: 50%;
  transition: .25s linear;
  margin: 0;
}

.todo-completed:hover {
  box-shadow: 0 0 10px rgba(51, 51, 51, 0.58);
}

.todo-completed:checked + .todo-content {
  text-decoration: line-through;
}

svg {
  border-radius: 50%;
  padding: 5px;
}

svg:hover {
  transition: .25s linear;
  border-radius: 50%;
  background-color: rgba(51, 51, 51, 0.26);
}

.todo-content {
  flex: 1;
  cursor: pointer;
  font-size: 14px;
  user-select: none;
}

.todo-priority {
  padding: 5px 10px;
  border-radius: 5px;
}

.todo-priority.medium {
  background-color: rgba(80, 161, 243, 0.1);
  border: 1px solid rgba(1, 93, 243);
  color: rgba(1, 93, 243);
  font-weight: 300;
}

.todo-priority.high {
  background-color: rgba(192, 0, 0, 0.1);
  border: 1px solid rgba(192, 0, 0);
  color: rgba(192, 0, 0);
  font-weight: 300;
}

.todo-priority.low {
  background-color: rgba(255, 234, 9, 0.1);
  border: 1px solid rgba(255, 228, 65);
  color: rgb(255, 228, 65);
  font-weight: 300;
}

.message {
  text-align-last: center;
}
</style>