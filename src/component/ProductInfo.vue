<script setup>
const props = defineProps({
  message: String,
});
</script>
<template>
  <h1>{{ message }}</h1>
</template>
