<script setup>
defineProps({
    items: {
        type: Array,
        required: true,
    },
})
</script>

<template>
    <div>
        <table>
            <tr
                v-for="item in items"
                :key="item.id"
            >
                <td>{{ item.id }}</td>
            </tr>
        </table>
    </div>
</template>

<style scoped></style>
