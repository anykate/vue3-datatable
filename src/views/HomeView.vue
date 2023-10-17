<script setup>
import DataTable from '@/components/DataTable.vue'
import { onMounted, onUnmounted, ref } from 'vue'

let items = ref([])

onMounted(async () => {
    const response = await fetch('http://localhost:3001/items')
    items.value = await response.json()
})

onUnmounted(() => {
    items.value = []
})
</script>

<template>
    <div class="min-h-screen bg-gray-100 p-8">
        <DataTable :items="items" />
    </div>
</template>

<style lang="scss" scoped></style>
