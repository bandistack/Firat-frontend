<script setup>
import { ref, onMounted } from 'vue'

const data = ref([])
onMounted(async () => {
  try {
    const res = await fetch('https://api.example.com/data')
    const json = await res.json()
    data.value = json
  } catch (error) {
    console.error('Error cargando datos:', error)
  }
})
</script>

<template>
    <table class="table-auto">
        <thead>
            <tr>
                <th>Title</th>
                <th>Summary</th>
                <th>Date</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(item, index) in data":key="index" class="border-t hover:bg-gray-50">
                <td>{{ item.col1 }}</td>
                <td>{{ item.col2 }}</td>
                <td>{{ item.col3 }}</td>
            </tr>
        </tbody>
    </table>    
</template>
