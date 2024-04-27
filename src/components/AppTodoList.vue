<script setup lang="ts">
import AppTodoItem from '@/components/AppTodoItem.vue'
import { computed, type PropType, ref } from 'vue'
import type { ITodo } from '@/types/ITodo'

const props = defineProps({
    todoList: {
        type: Object as PropType<ITodo[]>,
        required: true,
    }
});

const emit = defineEmits(['toggleTodoEmit', 'deleteTodo']);
const computedTodoList = computed(() => props.todoList);

const toggleTodo = (id: number) => emit('toggleTodoEmit', id);
const deleteTodo = (id: number) => emit('deleteTodo', id);
</script>

<template>
    <ul class="todo-list">
        <AppTodoItem
            v-for="todo in computedTodoList"
            :key="todo.id"
            :todo="todo"
            @toggleTodoEmit="toggleTodo"
            @deleteTodo="deleteTodo"
        />
    </ul>
</template>

<style scoped>

</style>