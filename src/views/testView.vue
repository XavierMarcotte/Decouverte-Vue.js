<script setup>
import { ref, onMounted } from "vue";
import ChildComp from "./ChildComp.vue";

const pElementRef = ref(null);

onMounted(() => {
  pElementRef.value.textContent = "monté!";
});

const childMsg = ref("Pas encore de message de l'enfant");
</script>

<template>
  <p ref="pElementRef">Hello</p>
  <ChildComp @response="(msg) => (childMsg = msg)" />
  <p>{{ childMsg }}</p>
</template>

<!-- Slot: https://fr.vuejs.org/tutorial/#step-14 -->
