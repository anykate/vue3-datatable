<script setup>
const emit = defineEmits(['search'])

const search = (e) => {
    emit('search', e.target.value)
}
</script>

<template>
    <form class="flex items-center px-4 py-3">
        <label
            for="search"
            class="sr-only"
            >Search</label
        >
        <div class="relative w-full">
            <input
                type="text"
                placeholder="Search..."
                id="search"
                @input="search"
                class="rounded-lg border border-gray-300 bg-gray-50 p-2 text-gray-900"
            />
        </div>
    </form>
</template>

<style scoped></style>
