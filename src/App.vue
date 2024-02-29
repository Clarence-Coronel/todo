<template>
<div class="bg-orange-300 w-full h-screen flex flex-col gap-10 items-center justify-start p-40">
    <h1 class="text-4xl text-neutral-800 font-bold">To Do List</h1>
    <form class="flex flex-nowrap items-center gap-4 w-full max-w-[400px]">
        <input v-model="todoInput" class="w-full focus:outline-none p-1 rounded-md bg-neutral-50 border border-neutral-400" type="text" name="todoInput" id="todoInput" placeholder="Wash clothes...">
        <button class="hover:bg-orange-500 duration-200 bg-orange-400 p-1 rounded-md w-fit" type="submit" @click.prevent="addTodo">
            <svg xmlns="http://www.w3.org/2000/svg" width="1.5rem" height="1.5rem" viewBox="0 0 24 24"><path fill="white" d="M11 13H5v-2h6V5h2v6h6v2h-6v6h-2z"/></svg>
        </button>
    </form>

    <div class="flex flex-col justify-start items-start w-full max-w-[400px] gap-2">
        <ToDo v-for="todo in todos" :key="todo.id" :id="todo.id" :content="todo.content" :isFinished="todo.isFinished" @toggled="toggleToDo" @remove="removeToDo" />
    </div>

    <MyFooter />
</div>
</template>

<script setup>
import { ref, watch } from 'vue';
import ToDo from './views/ToDo.vue'
import MyFooter from './components/MyFooter.vue'
import { generateUUID } from './composables/generateUUID.js'

const todoInput = ref("")

if(!localStorage.getItem("todos")) localStorage.setItem("todos", JSON.stringify([]))
const todos = ref(JSON.parse(localStorage.getItem("todos")))

const saveToDo = () => localStorage.setItem("todos", JSON.stringify(todos.value));
const addTodo = () => {
    if(todoInput.value == "") return
    const temp = {content: todoInput.value, isFinished: false, id: generateUUID()}
    todos.value.push(temp)
    saveToDo()
    todoInput.value = ""
}

const toggleToDo = (id) => {
    const index = todos.value.findIndex(obj => obj.id == id)
    todos.value[index].isFinished = !todos.value[index].isFinished
    saveToDo()
}

const removeToDo = (id) => {
    const temp = todos.value.filter(todo => todo.id != id)
    todos.value = temp
    saveToDo()
}

watch(todos.value, () => {
    console.log(todos.value)
})
</script>
