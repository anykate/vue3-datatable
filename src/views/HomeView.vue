<script setup>
import DataTable from '@/components/DataTable.vue'

const items = [
    {
        id: 1,
    },
    {
        id: 2,
    },
]
</script>

<style lang="scss" scoped></style>

<template>
    <div class="min-h-screen bg-gray-100 p-8">
        <DataTable :items="items" />
    </div>
</template>
