<script setup>
    import { ref, computed } from 'vue';
    const props = defineProps({
        todo: { text: String, isDone: Boolean, id: String}
    });
    const emit = defineEmits(['updateTodo', 'deleteTodo', 'toggleTodoStatus']);
    const editing = ref(false);
    const updateText = ref(""); 
    function handleUpdate(text, id){
        const updatedTodoText = text;
        if(updatedTodoText.length > 0){
            emit('updateTodo', updatedTodoText, id);
            editing.value = false;
        }
    } 
</script>

<template>
    <li>
      <form v-if="editing" @submit.prevent="(e) => handleUpdate(updateText, props.todo.id)" class='updateTodoItem'>
        <input class='updateTodoInput' v-model="updateText"/>
        <button type='submit' :disabled="updateText.length === 0">Update</button>
        <button type='button' @click="editing = false">Cancel</button>
      </form>
      <div v-else class='todoItem'>
        <p class='todoItemText' :class="{finishedTodo: props.todo.isDone}">{{ props.todo.text }}</p>
        <div class='todoItemBtns'>
          <button class='todoItemBtn' @click="() => emit('toggleTodoStatus', props.todo.id)">
            <svg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 24 24' stroke-width='1.5' stroke='currentColor' class='buttonSvg'>
              <path stroke-linecap='round' stroke-linejoin='round' d='m4.5 12.75 6 6 9-13.5' />
            </svg>
            Done
          </button>
          <button class='todoItemBtn' @click="() => {
            editing = true;
            updateText = props.todo.text;
            }">
            <svg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 24 24' stroke-width='1.5' stroke='currentColor' class='buttonSvg'>
              <path stroke-linecap='round' stroke-linejoin='round' d='m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L10.582 16.07a4.5 4.5 0 0 1-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 0 1 1.13-1.897l8.932-8.931Zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0 1 15.75 21H5.25A2.25 2.25 0 0 1 3 18.75V8.25A2.25 2.25 0 0 1 5.25 6H10' />
            </svg>
            Edit
          </button>
          <button class='todoItemBtn' @click="emit('deleteTodo', props.todo.id)">
            <svg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 24 24' stroke-width='1.5' stroke='currentColor' class='buttonSvg'>
              <path stroke-linecap='round' stroke-linejoin='round' d='m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0' />
            </svg>
            Delete
          </button>
        </div>
      </div>
    </li>
</template>

<style scoped>
.todoItem{
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: rgba(0,0,0,0.5);
  padding: 0.5rem;
  border-radius: 0.5rem;
}
.todoItemText{
  margin: 0;
  padding: 0.6em 1.2em;
  text-align: left;
}
.finishedTodo{
    text-decoration: line-through;
    opacity: 0.5;
}
.updateTodoItem{
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: rgba(0,0,0,0.5);
  gap: 0.5rem;
  padding: 0.5rem;
  border-radius: 0.5rem;
}
.todoItemBtns{
  display: flex;
  gap: .5rem;
}
.todoItemBtn{
  display: flex;
  justify-content: center;
  align-items: center;
  gap: .25rem;
}
.buttonSvg{
  stroke: white;
  height: 1rem;
  width: 1rem;
}
.updateTodoInput{
  padding: 0.6em 1.2em;
  width: 100%;
}
</style>
