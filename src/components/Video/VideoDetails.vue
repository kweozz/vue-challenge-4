<script setup>
//PROPS title
const props = defineProps({
  title: String,
});
</script>

<template>
  <h1>{{ title }}</h1>
</template>

<style scoped></style>
