<template>
<div class="flex flex-row flex-nowrap justify-start items-center gap-2 w-full">
    <button @click="toggleTodoStatus" class="hover:border-neutral-400 hover:cursor-pointer duration-200 w-5 h-5 border-2 border-neutral-500 rounded-sm">
        <svg v-show="isFinished" xmlns="http://www.w3.org/2000/svg" width="1rem" height="1rem" viewBox="0 0 20 20"><path fill="currentColor" d="M8.294 16.998c-.435 0-.847-.203-1.111-.553L3.61 11.724a1.392 1.392 0 0 1 .27-1.951a1.392 1.392 0 0 1 1.953.27l2.351 3.104l5.911-9.492a1.396 1.396 0 0 1 1.921-.445c.653.406.854 1.266.446 1.92L9.478 16.34a1.39 1.39 0 0 1-1.12.656c-.022.002-.042.002-.064.002"/></svg>
    </button>
    <div :class="{'line-through': isFinished}" class="decoration-red-500 decoration-2 w-fit text-left font-semibold text-lg text-neutral-800">{{ content }}</div>
    <button class="w-fit" @click="removeTodoItem">
        <svg xmlns="http://www.w3.org/2000/svg" width="0.7rem" height="0.7rem" viewBox="0 0 14 14"><path fill="red" fill-rule="evenodd" d="M1.707.293A1 1 0 0 0 .293 1.707L5.586 7L.293 12.293a1 1 0 1 0 1.414 1.414L7 8.414l5.293 5.293a1 1 0 0 0 1.414-1.414L8.414 7l5.293-5.293A1 1 0 0 0 12.293.293L7 5.586z" clip-rule="evenodd"/></svg>    
    </button>
</div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const emit = defineEmits();
const props = defineProps({
    content: {
        type: String
    },
    isFinished: {
        type: Boolean
    },
    id: {
        type: String
    }
})



const toggleTodoStatus = () => {
    emit('toggled', props.id)
}

const removeTodoItem = () => {
    emit('remove', props.id)
}
</script>