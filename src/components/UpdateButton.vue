<template>
    <button type="button" @click="handleUpdate">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="#45a3e2d5" class="del-btn">
            <path stroke-linecap="round" stroke-linejoin="round" d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L6.832 19.82a4.5 4.5 0 0 1-1.897 1.13l-2.685.8.8-2.685a4.5 4.5 0 0 1 1.13-1.897L16.863 4.487Zm0 0L19.5 7.125" />
        </svg>
    </button>
</template>

<script setup>
const emit = defineEmits(['handleUpdate'])
const handleUpdate = () => {
    emit('handleUpdate')
}
</script>

<style scoped>
.del-btn {
    width: 20px;
    height: 20px;
    background-color: transparent;
}    
</style>