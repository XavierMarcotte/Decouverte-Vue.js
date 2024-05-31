<script setup>
const emit = defineEmits(["response"]);

emit("response", "hello à partir de l'enfant");
</script>

<template>
  <h2>Composant enfant</h2>
</template>
