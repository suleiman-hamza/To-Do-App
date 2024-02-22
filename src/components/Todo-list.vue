<script setup>
import AddButton from './AddButton.vue';
import Lists from './Lists.vue';

import { ref, onMounted, watch, computed } from 'vue'

onMounted(() => {
    todos.value = JSON.parse(localStorage.getItem('todos')) || [];
    targetArray.value = JSON.parse(localStorage.getItem('Completed')) || [];
})

const todo = ref('')
const todos = ref([])
const count = ref(0)

// completed task array
const targetArray = ref([])

watch(todos, (newValue) =>  {
    localStorage.setItem('todos', JSON.stringify(newValue))
}, { deep:true })

watch(count, newValue => {
    localStorage.setItem('Count', newValue)
})

watch(targetArray, (newValue) => {
    localStorage.setItem('Completed', JSON.stringify(newValue))
}, { deep: true })

const addMyTodo = (message) => {
// check if todo entry is empty, then push the entered todo text and other properties
    if (todo.value.trim() !== "") {
        todos.value.unshift({
            text: todo.value,
            isEditng: false,
            editedText: "",
            done: false
        })
    } else {
        alert('enter valid string')
    }
    todo.value = "";
}

// move handler to push out an element to the completed section
const move = (index) => { 
    if (todos.value[index].done) {
        const itemToMove = todos.value[index]
        console.log(itemToMove) // comment: itemToMove targets an elem from todos using index param
        todos.value.splice(index, 1)

        pushItem(itemToMove)
    }
}

// this part actually does the job of pushing to the completed section
const pushItem = (item) =>{
    targetArray.value.unshift(item)
}

// undo handler to push from targetArray back to original todos Array
const undoMove = (index) => {
    console.log(index)
    if (!targetArray.value[index].done) {
        const moveElem = targetArray.value[index]
        targetArray.value.splice(index, 1)

        undoItem(moveElem)
    }
}

const undoItem = (item) => {
    todos.value.unshift(item)
}
</script>

<template>
    <section class="input-area">
        <label for="input">Enter a Task</label>
        <input type="text" id="input" v-model="todo" @keyup.enter="addMyTodo(message)">
        <AddButton @add-todo="addMyTodo" />
    </section>
    <section>
        <h2>To-do List</h2>
        <ul class="list">
            <Lists :todo="todo" :todos="todos" :targetArray="targetArray" @handle-move="move"/>
        </ul>
    </section>
    <section class="completed">
        <h3>Completed</h3>
        <ul>
            <li v-for="(alias, index) in targetArray">
                <input type="checkbox" @change="undoMove(index)" name="checkbox" v-model="alias.done">
                <span>{{ alias.text }}</span>
                <!--delte later v-model value of -->
                <p>{{ alias.done }}</p>
            </li>
        </ul>
    </section>
</template>

<style scoped>
label, .completed li {
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