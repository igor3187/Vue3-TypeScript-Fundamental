<script setup lang="ts">
import { type PropType } from 'vue'
import type { IStatisticInfo } from '@/types/IStatisticInfo'

defineProps({
    todoInfo: {
        type: Object as PropType<IStatisticInfo>,
        required: true,
    }
});
</script>

<template>
    <footer class="app-footer">
        Active: {{todoInfo.active}} Done: {{todoInfo.done}}
    </footer>
</template>

<style scoped>

</style>