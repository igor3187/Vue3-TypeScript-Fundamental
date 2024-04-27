<script setup lang="ts">
import { type PropType, ref } from 'vue'
import type { TFilterStatusType } from '@/types/TFilterStatusType'
import type { IFilterStatus } from '@/types/IFilterStatus'

const props = defineProps({
    activeFilter: {
        type: String as PropType<TFilterStatusType>,
        required: true,
    }
});

const filters = ref<IFilterStatus>({
    filters: ['All', 'Active', 'Done']
});

const isActive = ref(props.activeFilter);
const emit = defineEmits(['setFilter']);

const setFilter = (status: TFilterStatusType) => {
    emit('setFilter', status);
    return isActive.value = status
}
</script>

<template>
    <aside class="app-filters">
        <section class="toggle-group">
            <button v-for="(filter, index) in filters.filters"
                    :key="index"
                    class="button"
                    :class="{'button--primary' : isActive === filter}"
                    @click="setFilter(filter)"
            >
                {{ filter }}
            </button>
        </section>
    </aside>
</template>

<style scoped>

</style>