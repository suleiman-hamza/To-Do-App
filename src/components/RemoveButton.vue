<template>
    <button type="button" @click="removeTodo">Del</button>
</template>

<script setup>
//next props and emitting
const props = defineProps({
    todo: String,
    todos: Array
})
const emit = defineEmits(['removeTodo'])

const removeTodo = () => {
    emit('removeTodo')
}

</script>