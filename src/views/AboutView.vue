<script setup>
import { ref, computed } from "vue";

let id = 0;

const newTodo = ref("");
const hideCompleted = ref(false);
const html = ref("<button>Cliquez moi!</button>");
const todos = ref([
  { id: id++, text: "Apprendre le HTML", done: true },
  { id: id++, text: "Apprendre le JavaScript", done: true },
  { id: id++, text: "Apprendre Vue", done: false },
]);

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}
</script>

<template>
  <!-- Pour les failles xss, utiliser v-html -->
  <div v-html="html"></div>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="Nouvelle tâche" />
    <button>Ajouter une tâche</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? "Afficher toutes" : "Cacher complétées" }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
