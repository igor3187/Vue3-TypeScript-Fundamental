<script setup lang="ts">
import type { PropType } from 'vue'
import type { ITodo } from '@/types/ITodo'

defineProps({
   todo: {
       type: Object as PropType<ITodo>,
       required: true,
   },
});

const emit = defineEmits(['toggleTodoEmit', 'deleteTodo']);

const toggleTodo = (id: undefined | number) => emit('toggleTodoEmit', id);
const deleteTodo = async (id: undefined | number) => emit('deleteTodo', id);
</script>

<template>
    <li class="todo-item" :class="{'todo-item--done' : todo.completed}" @click="toggleTodo(todo.id)">
        <div class="todo-item__status">
            <i class="bi bi-check2" />
        </div>
        <span class="todo-item__text">{{ todo.text }}</span>
        <button class="todo-item__remove-button" @click.stop="deleteTodo(todo.id)">
            <i class="bi bi-trash3" />
        </button>
    </li>
</template>

<style scoped>

</style>