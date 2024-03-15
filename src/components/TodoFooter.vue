<script setup>
  defineProps(['year', 'name']);
  const emit = defineEmits(['increaseYear']);
</script>

<template>
  <hr>
  <button @click="emit('increaseYear', 1)">연도를 1년 증가시키기</button>
  <h3>Copyright {{ year }} by {{ name }}</h3>
</template>

<style scoped>

</style>