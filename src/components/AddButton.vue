<template>
    <button @click="addTodo" >Add</button>
</template>

<script setup>

    const emit = defineEmits(['addTodo'])
    function addTodo() {
        emit('addTodo', 'added post');
    }
</script> 
<style scoped>
button {
    color: beige;
    padding: 0.5rem 0.75rem;
    background-color: rgba(69, 163, 226, 0.836);
    border: none;
    font-weight: 700;
}
</style>