<script setup>
const props = defineProps({
  title: String
})
</script>

<template>
  <div class="card-container">
    <h2>{{ props.title }}</h2>
    <p>importante!</p>
  </div>
</template>

<style scoped>
.card-container {
  background-color: gray;
  padding: 10px;
  cursor: default;
}
</style>
