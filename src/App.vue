<script setup>
import axios from 'axios';
import { onMounted, ref, watch } from 'vue';
import TodoHeader from './components/TodoHeader.vue';
import TodoFooter from './components/TodoFooter.vue'
import TodoMain from './components/TodoMain.vue'

// states
const title = ref('Todo 관리');
const year = ref(2024);
const developerName = ref('choi');
const todos = ref([]);  // { value : [] }
// const todos = reactive([]);

// year 값이 바뀌면 todos 데이터를 가져오기
watch(year, async (newYear) => {
  const res = await axios.get('https://jsonplaceholder.typicode.com/todos')
  console.log('watch 함수 호출됨')
  todos.value = res.data;
})

// 화면이 로딩된 직후에 실행되는 훅 (콜백함수)
onMounted(async () => {
  // axios.get('https://jsonplaceholder.typicode.com/todos')
  // .then(res => todos.value = res.data)
  const res = await axios.get('https://jsonplaceholder.typicode.com/todos');
  todos.value = res.data 
})

// 이벤트 처리 코드
function getTodoButtonClick(){
  //promise 방식
  fetch('https://jsonplaceholder.typicode.com/todos')
  .then(result => result.json())
  .then(json => todos.value = json)
}

// year 값을 바꾸는 함수
function yearButtonClicked() {
  year.value++;
}
// increaseYear 이벤트가 발생했을 때 처리
function increaseYearFired(event){
  console.log('increase year event fired' + event);
  year.value = year.value + event;
}
</script>

<template>
  <todo-header :title="title">
    <p>헤더 컴포넌트로 컨텐츠를 전달</p>
  </todo-header>
  
  <todo-main :todos="todos"></todo-main>

  <todo-footer :year="year" :name="developerName" @increaseYear="increaseYearFired"></todo-footer>
</template>

<style scoped>

</style>
