<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';

const todos = ref([]);

function getTodoButtonClick(){
  //promise 방식
  fetch('https://jsonplaceholder.typicode.com/todos')
  .then(result => result.json())
  .then(json => todos.value = json)
}

onMounted(async () => {
  // axios.get('https://jsonplaceholder.typicode.com/todos')
  // .then(res => todos.value = res.data)
  
  const res = await axios.get('https://jsonplaceholder.typicode.com/todos');
  todos.value = res.data 
})

const year = ref(2024)
function yearButtonClicked() {
  year.value++;
}

</script>

<template>
  <h1>Todos</h1>
  <hr>
  
  <button @click="getTodoButtonClick">할일 목록 가져오기</button>
  <h3>할일 목록</h3>
  <ul>
    <li v-for="todo in todos" :key="todo.userId">
      {{ todo.title }} - {{ todo.completed ? '완료' : '진행중' }}
    </li>
  </ul>
  <hr>

  <button @click="yearButtonClicked">연도를 1년 증가시키기</button>
  <h3>Copyright {{ year }} by choi</h3>
</template>

<style scoped>

</style>
