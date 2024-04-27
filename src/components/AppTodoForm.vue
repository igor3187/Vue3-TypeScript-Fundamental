<script setup lang="ts">
import { ref } from 'vue';
import type { ITodoFormState } from '@/types/ITodoFormState';

const emit = defineEmits(['newTodo']);
const isFormVisible = ref(false as ITodoFormState['isFormVisible']);
const todoItemText = ref('' as ITodoFormState['todoItemText']);

const showAddTodoForm = () => isFormVisible.value = true;
const hideAddTodoForm = () => isFormVisible.value = false;

const addTodoHandler = () => {
    emit('newTodo', {
        id: new Date().getTime(),
        text: todoItemText.value,
        completed: false,
    });

    todoItemText.value = '';
}
</script>

<template>
    <section class="add-todo">
        <form v-if="isFormVisible" class="add-todo__form" @submit.prevent="addTodoHandler">
            <button class="close-button" type="button" @click="hideAddTodoForm">
                <i class="bi bi-x"></i>
            </button>
            <div class="text-input text-input--focus">
                <input class="input" v-model="todoItemText" @submit.prevent="addTodoHandler" />
            </div>
            <button class="button button--filled">Add task</button>
        </form>
        <button v-else class="add-todo__show-form-button" @click="showAddTodoForm">
            <i class="bi bi-plus-lg"></i>
        </button>
    </section>
</template>

<style scoped>

</style>