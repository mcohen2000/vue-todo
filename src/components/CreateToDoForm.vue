<script setup>
    import { ref } from 'vue';
    const emit = defineEmits(["createTodo"])
    const todoInputText = ref("")
    function handleSubmit(){
        const newTodoText = todoInputText.value;
        if(newTodoText.length > 0){
            emit('createTodo', newTodoText);
        }
        todoInputText.value = "";
    } 
</script>

<template>
    <form class="newTodoForm" @submit.prevent="handleSubmit">
        <input class="newTodoInput" v-model="todoInputText"/>
        <button type="submit">Submit</button>
    </form>
</template>

<style scoped>
.newTodoForm{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 1rem;

}
.newTodoInput{
    padding: 0.6em 1.2em;
 }
</style>
