<script setup>
import { ref } from 'vue'
import TodoItem from '@/components/TodoItem.vue'

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
    <button>Add Todo</button>
  </form>
  <ul>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :text="todo.text"
      @delete="removeTodo(todo)"
    />
  </ul>
</template>
