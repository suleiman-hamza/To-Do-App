<template>
    <button type="button" @click="editTodo">Edit</button>
</template>

<script setup>

const emit = defineEmits(['editTodo'])

const editTodo = () => {
    emit('editTodo')
}

</script>