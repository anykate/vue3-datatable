<script setup>
import { computed, ref } from 'vue'

const show = ref(false)

const props = defineProps({
    items: {
        type: Array,
        required: true,
    },
})

const emit = defineEmits(['filter', 'reset-status-list'])

const statusList = computed(() => {
    return [...new Set(props.items.map((item) => item.status))]
})

const filter = (e) => {
    emit('filter', e.target.value)
}

const handleBtnClick = () => {
    show.value = !show.value
    emit('reset-status-list', true)
}
</script>

<template>
    <div class="relative flex w-full items-center px-4">
        <button
            class="flex w-full items-center px-4 py-2 text-sm font-medium text-gray-900 focus:outline-4"
            @click="handleBtnClick"
        >
            Filter
        </button>
        <div
            v-if="show"
            class="absolute right-0 top-12 z-10 mt-3 w-48 rounded-lg bg-white p-3 shadow"
        >
            <h6 class="mb-3 text-sm font-medium text-gray-900">Status</h6>
            <ul class="space-y-2 text-sm">
                <li
                    v-for="(status, index) in statusList"
                    :key="index"
                >
                    <input
                        :id="`filter_option_{index}`"
                        type="checkbox"
                        :value="status"
                        @change="filter"
                    />
                    <label
                        :for="`filter_option_{index}`"
                        class="ml-2 text-sm font-medium text-gray-900"
                        >{{ status }}</label
                    >
                </li>
            </ul>
        </div>
    </div>
</template>

<style scoped></style>
