<script setup>
import AddButton from './AddButton.vue';
import Lists from './Lists.vue';

import { ref, onMounted } from 'vue'

onMounted(() => {
    const collect = localStorage.getItem('saved')
    console.log(collect)
    let parse = JSON.parse(collect)
    console.log(parse)
    todos.value = parse
})

const todo = ref('')
const todos = ref([
    {
        text: 'addidas',
        isEditng: false,
        editedText: ""
    },
    {
        text: 'puma',
        isEditng: false,
        editedText: ""
    }
])

// create a function to encapsulate this tasks
function handleStuff() {
    const stringify = JSON.stringify(todos.value)
    console.log(stringify)

    localStorage.setItem('saved', stringify)
}

const addMyTodo = (message) => {
// delete this console later: emitted event argument
    console.log(message)
// check if todo entry is empty, then push the entered todo text and other properties
    if (todo.value.trim() !== "") {
        todos.value.push({
            text: todo.value,
            isEditng: false,
            editedText: ""
        })
    } else {
        alert('enter valid string')
    }
    todo.value = "";
    handleStuff();
}
</script>

<template>
    <section class="input-area">
        <label for="input">Enter a Task</label>
        <input type="text" id="input" v-model="todo" @keyup.enter="addMyTodo">
        <AddButton @add-todo="addMyTodo" />
    </section>
    <section>
        <h2>To-do List</h2>
        <ul class="list">
            <Lists :todo="todo" :todos="todos"/>
        </ul>
    </section>
</template>

<style scoped>
label {
    display: block;
    font-size: 1.25rem;
    padding-bottom: 0.5rem;
    color: rgba(69, 163, 226, 0.836);
}
input {
    padding: 1rem;
    border: 1px solid grey;
    background-color: rgba(26, 26, 23, 0.637);
    font-size: 1rem;
    color: rgb(207, 169, 119);
    border-radius: 5px;
    outline: none;
    margin-right: 1.5rem;
}
input:is(:focus, :hover) {
    border-color: rgba(69, 163, 226, 0.836);
}
ul {
    padding: 1rem;
    border: 1px solid grey;
    border-radius: 5px;
}
.input-area {
    padding: 1rem;
    border: 1px solid grey;
    border-radius: 10px;
}
</style>