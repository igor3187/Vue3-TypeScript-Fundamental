<script setup lang="ts">
import AppHeader from '@/components/AppHeader.vue'
import AppFilters from '@/components/AppFilters.vue'
import AppTodoList from '@/components/AppTodoList.vue'
import AppTodoForm from '@/components/AppTodoForm.vue'
import AppFooter from '@/components/AppFooter.vue'
import type { ITodo } from '@/types/ITodo'
import { computed, ref } from 'vue'
import type { TFilterStatusType } from '@/types/TFilterStatusType'
import type { IStatisticInfo } from '@/types/IStatisticInfo'

const currentFilter = ref<TFilterStatusType>('All');
const computedActiveTodos = computed(() => todosList.value.filter(item => !item.completed));
const computedCompletedTodos = computed(() => todosList.value.filter(item => item.completed));

const todosList = ref<ITodo[]>([
    {id: 1, text: 'ITodo 1', completed: true},
    {id: 2, text: 'ITodo 2', completed: false},
    {id: 3, text: 'ITodo 3', completed: false},
]);

const addNewTodo = (todo: ITodo) => todosList.value.push(todo);
const deleteTodo = async (id: ITodo) => todosList.value.splice(todosList.value.indexOf(id), 1);
const setFilter = (status: TFilterStatusType) => currentFilter.value = status;
const changeStatus = (todoId: ITodo) => todosList.value.find(item => {
    if(item.id === todoId) item.completed = !item.completed
});

const computedFilteredTodo = computed<ITodo[]>(() => {
    switch (!!currentFilter.value) {
        case currentFilter.value === 'Active':
            return computedActiveTodos.value;
        case currentFilter.value === 'Done':
            return computedCompletedTodos.value;
        default:
            return todosList.value;
    }
});

const computedStatistics = computed<IStatisticInfo>(() => {
    return {
        active: computedActiveTodos.value.length,
        done: computedCompletedTodos.value.length,
    }
});
</script>

<template>
    <div id="app">
        <AppHeader />
        <AppFilters :active-filter="currentFilter" @setFilter="setFilter"/>
        <main class="app-main">
            <AppTodoList :todoList="computedFilteredTodo" @deleteTodo="deleteTodo" @toggleTodoEmit="changeStatus" />
            <AppTodoForm @newTodo="addNewTodo" />
        </main>
        <AppFooter :todoInfo="computedStatistics"/>
    </div>
</template>

<style scoped>

</style>
