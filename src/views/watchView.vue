<script setup>
import { ref, watch } from "vue";

const todoId = ref(1);
const todoData = ref(null);

async function fetchData() {
  todoData.value = null;
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  );
  todoData.value = await res.json();
}

fetchData();

watch(todoId, fetchData);
</script>

<template>
  <p>Id de la liste de tâches: {{ todoId }}</p>
  <button @click="todoId++" :disabled="!todoData">
    Récupérer la prochaine liste de tâches
  </button>
  <p v-if="!todoData">Chargement...</p>
  <pre v-else>{{ todoData }}</pre>
</template>
