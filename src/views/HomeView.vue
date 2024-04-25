<script setup>
import { ref } from 'vue'

// give each todo a unique id
let id = 0

const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
  { id: id++, text: 'Learn Vue' }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todoToRemove) {
  todos.value = todos.value.filter(function (todo) {
    return todo.id != todoToRemove.id
  })
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="new todo" />
    <button class="add-todo">Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button class="remove-todo" @click="removeTodo(todo)">x</button>
    </li>
  </ul>
</template>

<style>
button {
  background-color: #41b883;
  color: white;
  border: none;
  border-radius: 2px;
}

.add-todo {
  padding: 3px 6px;
}

.remove-todo {
  margin-left: 8px;
  margin-top: 4px;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  max-width: 200px;
}
</style>
