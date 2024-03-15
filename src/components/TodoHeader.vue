<script setup>
  defineProps(['title'])
</script>

<template>
  <h1>{{ title }}</h1>
  <hr>
  <slot>아무 컨텐츠도 전달 안될 때 나오는 컨텐츠입니당</slot>
  <hr>
</template>

<style scoped>

</style>