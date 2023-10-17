<script setup>
const emit = defineEmits(['filter'])

const filter = (e) => {
    emit('filter', e.target.value)
}
</script>

<template>
    <div></div>
    <label
        for="all"
        class="mr-4 flex flex-nowrap items-center"
    >
        <input
            id="all"
            type="radio"
            name="show"
            checked
            value="all"
            @change="filter"
        />
        <span class="ml-1 whitespace-nowrap">Show All</span>
    </label>
    <label
        for="today"
        class="mr-4 flex flex-nowrap items-center"
    >
        <input
            id="today"
            type="radio"
            name="show"
            value="today"
            @change="filter"
        />
        <span class="ml-1 whitespace-nowrap">Due Today</span>
    </label>
    <label
        for="past"
        class="mr-4 flex flex-nowrap items-center"
    >
        <input
            id="past"
            type="radio"
            name="show"
            value="past"
            @change="filter"
        />
        <span class="ml-1 whitespace-nowrap">Past Due</span>
    </label>
    <label
        for="future"
        class="mr-4 flex flex-nowrap items-center"
    >
        <input
            id="future"
            type="radio"
            name="show"
            value="future"
            @change="filter"
        />
        <span class="ml-1 whitespace-nowrap">Due Ahead</span>
    </label>
</template>

<style scoped></style>
