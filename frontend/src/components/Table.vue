<script setup>
import { ref, onMounted } from 'vue'
import { computed } from "vue";
import axios from 'axios'

const data = ref([])
const loading = ref(true)
const error = ref(null)
const columns = computed(() => (data.value.length ? Object.keys(data.value[0]) : []))

onMounted(async () => {
  try {
    const res = await axios.get('http://192.168.1.8:8000/rss/today')
    data.value = res.data
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
})
</script>

<template>
  <div class="px-6 py-4">
    <p v-if="loading" class="text-gray-500">Getting data...</p>
    <p v-else-if="error" class="text-red-500">Error: {{ error }}</p>
    <table v-else class="table-auto w-full border border-gray-200 rounded-lg shadow-sm">
      <thead class="bg-gray-100">
        <tr>
            <th v-for="col in columns" :key="col" class="px-4 py-2 text-left">
                {{ col }}
            </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, rowIndex) in data"
          :key="rowIndex"
          class="border-t hover:bg-gray-50">
            <td
                v-for="(value, colIndex) in item"
                :key="colIndex"
                class="px-4 py-2 text-sm text-gray-800">
                {{ value }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
