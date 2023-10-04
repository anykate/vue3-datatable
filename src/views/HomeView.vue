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
    <div class="p-8 bg-gray-100 min-h-screen">
        <DataTable :items="items" />
    </div>
</template>
