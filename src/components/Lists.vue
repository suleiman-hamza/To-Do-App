<template>
    <li v-for="(item, index) in todos" :key="index">
        <span v-if="!item.isEditng" >
            {{ item.text }}
        </span>
        <input 
            type="text"
            v-if="item.isEditng" 
            v-model="item.editedText" 
            @keyup.enter="updateTodo(index)"
        >
        <div class="btn-container">
            <RemoveButton :todo="todo" :todos="todos" @remove-todo="remove(index)" />
            <EditButton @edit-todo="edit(index)" v-if="!item.isEditng"/>
            <UpdateButton @handle-update="handle(index)" v-if="item.isEditng"/>
        </div>
    </li>
</template>

<script setup>
import RemoveButton from './RemoveButton.vue'
import EditButton from './EditButton.vue'
import UpdateButton from './UpdateButton.vue'

let props = defineProps({
    todo: String,
    todos: Array
})

// delete a task, emmitted from removebutton.vue,
//confirm delete then use array splice methhod withindex to delete.
const remove = (index) => {
    console.log(index)
    let confirmDelete = confirm('are you sure you wanna delete this ?')
    if (confirmDelete) {
        props.todos.splice(index, 1)
    }
}
// edit a task, func emitted from EditButton.vue,
// use index of todos object to modify the properties,
//
function edit(index) {
    console.log(index)
    props.todos[index].isEditng = true
    props.todos[index].editedText = props.todos[index].text
}

const handle = (index) => {
    updateTodo(index)
}

const updateTodo = (index) => {
    console.log(index)
    if (props.todos[index].editedText) {
        props.todos[index].text = props.todos[index].editedText
        props.todos[index].isEditng = false
        props.todos[index].editedText = ""
    } else {
        alert('please enter an item')
    }
}
</script>
<style scoped>
li {
    list-style-type: none;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    font-size: 1.15rem;
    border: 1px solid rgba(69, 163, 226, 0.836);
    border-radius: 5px;
    background-color: rgba(146, 155, 155, 0.226);
    margin-block: 0.5rem;
    /* transition: transform 300ms ease-in; */
}
.btn-container {
    display: flex;
    gap: 1rem;
}
</style>