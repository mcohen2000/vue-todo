<script setup>
import { v4 as uuid } from 'uuid';
import CreateToDoForm from './components/CreateTodoForm.vue';
import ToDoItem from './components/ToDoItem.vue'
import { ref } from 'vue';

const todoList = ref([]);

function createTodo(text){
  todoList.value.push({text, isDone: false, id: uuid()})
}
function updateTodo(text, id){
  const listCopy = todoList.value;
  todoList.value = listCopy.map(item => 
    item.id === id ? {...item, text} : item
  )
}
function toggleTodo(id){
  const listCopy = todoList.value;
  todoList.value = listCopy.map(item => 
    item.id === id ? {...item, isDone: !item.isDone} : item
  )
}
function deleteTodo(id){
  todoList.value = todoList.value.filter(item => item.id !== id)
}

</script>

<template>
  <img class='vueLogo' src='./assets/vue.svg' alt='Vue Logo'>
  <h1>Vue To Do</h1>
  <CreateToDoForm @createTodo="(str) => createTodo(str)"/>
  <ul class='todoList'>
    <ToDoItem v-for="todo in todoList" :key="todo.id" :todo="todo" @updateTodo="(text, id) => updateTodo(text, id)" @deleteTodo="(id) => deleteTodo(id)" @toggleTodoStatus="(id) => toggleTodo(id)"/>
  </ul>
 <div>

 </div>
</template>

<style scoped>
.vueLogo{
  height: 5rem;
}
.todoList{
  display: flex;
  flex-direction: column-reverse;
  gap: .5rem;
  padding: 0;
  list-style: none;
}


</style>
