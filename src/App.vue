<script setup>
import { v4 as uuid } from 'uuid';
import CreateToDoForm from './components/CreateTodoForm.vue';
import { ref } from 'vue';

const todoList = ref([]);

function createTodo(text){
  todoList.value.push({text, isDone: false, id: uuid()})
}

</script>

<template>
  <img class='vueLogo' src='./assets/vue.svg' alt='Vue Logo'>
  <h1>Vue To Do</h1>
  <CreateToDoForm @createTodo="(str) => createTodo(str)"/>
  <ul>
    <li v-for="todo in todoList" :key="todo.id">{{ todo.text }}</li>
  </ul>
 <div>

 </div>
</template>

<style scoped>

 .vueLogo{
  height: 5rem;
 }
</style>
