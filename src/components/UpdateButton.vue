<template>
    <button type="button" @click="handleUpdate">Update</button>
</template>

<script setup>
const emit = defineEmits(['handleUpdate'])
const handleUpdate = () => {
    emit('handleUpdate')
}
</script>