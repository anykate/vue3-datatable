<script setup>
import FilterDropdown from '@/components/FilterDropdown.vue'
import FilterRadios from '@/components/FilterRadios.vue'
import SearchForm from '@/components/SearchForm.vue'
import { computed, ref } from 'vue'

const searchFilter = ref('')
const radioFilter = ref('')
const statusListFilter = ref([])

const props = defineProps({
    items: {
        type: Array,
        required: true,
    },
})

const filteredItems = computed(() => {
    let items = props.items

    switch (radioFilter.value) {
        case 'today':
            // show items due today
            items = items.filter((item) => new Date(item.due_at) === new Date())
            break

        case 'past':
            // show items past due
            items = items.filter((item) => new Date(item.due_at) < new Date())
            break

        case 'future':
            // show items due after today
            items = items.filter((item) => new Date(item.due_at) > new Date())
            break

        default:
            break
    }

    if (statusListFilter.value.length) {
        items = items.filter((item) =>
            statusListFilter.value.includes(item.status)
        )
    }

    if (searchFilter.value.trim().length === 0) return items

    return items.filter(
        (item) =>
            item.title
                .toLowerCase()
                .includes(searchFilter.value.trim().toLowerCase()) ||
            item.user.name
                .toLowerCase()
                .includes(searchFilter.value.trim().toLowerCase())
    )
})

const handleSearch = (search) => {
    searchFilter.value = search
}

const handleRadioFilter = (filter) => {
    radioFilter.value = filter
}

const handleCheckboxFilter = (filter, m) => {
    if (statusListFilter.value.includes(filter)) {
        return statusListFilter.value.splice(
            statusListFilter.value.indexOf(filter),
            1
        )
    }

    return statusListFilter.value.push(filter)
}

const handleResetStatusList = (check) => {
    if (check) {
        statusListFilter.value = []
    }
}
</script>

<template>
    <div class="relative rounded-lg border bg-white">
        <div class="mt-3 pl-3 text-sm text-gray-500">
            Records# {{ filteredItems.length }}
        </div>
        <div class="flex items-center justify-between">
            <!-- Search bar -->
            <SearchForm @search="handleSearch" />
            <div class="text-2xl font-extrabold"></div>
            <div
                class="mr-5 flex text-sm font-semibold max-md:flex-col max-md:justify-center max-md:space-y-3 md:flex-row md:items-center md:justify-end"
            >
                <!-- Radio buttons -->
                <FilterRadios @filter="handleRadioFilter" />
                <!-- List of filters for statuses -->
                <FilterDropdown
                    :items="items"
                    @filter="handleCheckboxFilter"
                    @reset-status-list="handleResetStatusList"
                />
            </div>
        </div>
        <table class="w-full text-left text-sm text-gray-500">
            <thead class="bg-gray-50 text-xs uppercase text-gray-700">
                <tr>
                    <th class="px-4 py-3">ID</th>
                    <th class="px-4 py-3">Assigned To</th>
                    <th class="px-4 py-3">Status</th>
                    <th class="px-4 py-3">Title</th>
                    <th class="px-4 py-3">Due At</th>
                    <th class="px-4 py-3">
                        <span class="sr-only">Actions</span>
                    </th>
                </tr>
            </thead>
            <tr
                v-for="item in filteredItems"
                :key="item.id"
                class="border-b"
            >
                <td class="px-4 py-3 font-medium text-gray-900">
                    {{ item.id }}
                </td>
                <td class="px-4 py-3">
                    {{ item.user.name }}
                </td>
                <td class="px-4 py-3">
                    {{ item.status }}
                </td>
                <td class="px-4 py-3">
                    {{ item.title }}
                </td>
                <td class="px-4 py-3">
                    {{ item.due_at }}
                </td>
                <td class="flex items-center justify-end px-4 py-3">
                    <router-link
                        :to="{ name: 'home' }"
                        class="text-indigo-500 hover:underline"
                    >
                        Details
                    </router-link>
                </td>
            </tr>
        </table>
    </div>
</template>

<style scoped></style>
