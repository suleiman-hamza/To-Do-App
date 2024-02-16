<script setup>
import TodoList from '@/components/Todo-list.vue'

</script>

<template>
  <main>
    <h1 class="title">To-Do App</h1>
    <Todo-list />
  </main>
</template>

<style>
  .title {
    text-align: center;
    color: rgba(69, 163, 226, 0.836);
    font-size: 1.75rem;
    padding: 1rem;
    border: 1px solid rgba(69, 163, 226, 0.836);
    height: 100px;
  }
  button {
    color: beige;
    padding: 0.5rem 0.75rem;
    background-color: rgba(69, 163, 226, 0.836);
    border: none;
    font-weight: 700;
}
</style>
