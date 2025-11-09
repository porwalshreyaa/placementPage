
<script setup>
import { ref } from 'vue'

const AZUL = '#1D5DEC'

const bar = ref({
  series: [{ name: 'Placements', data: [40, 30, 25, 20] }],
  options: {
    chart: { toolbar: { show: false } },
    colors: [AZUL],
    xaxis: { categories: ['CSE', 'ECE', 'IT', 'ME'] },
  },
})

const pie = ref({
  series: [44, 25, 15, 16],
  options: {
    labels: ['TCS', 'Infosys', 'Wipro', 'IBM'],
    colors: [AZUL, '#4A90E2', '#7BAAF7', '#AFC6FB'],
    legend: { position: 'bottom' },
  },
})
</script>



<template>
    <section class="grid gap-6 md:grid-cols-2">
      <div class="bg-white rounded-2xl shadow-sm p-4 border border-gray-100">
        <h3 class="text-lg font-semibold mb-2 text-azul-500">Placements by Department</h3>
        <apexchart type="bar" width="100%" :options="bar.options" :series="bar.series" />
      </div>
  
      <div class="bg-white rounded-2xl shadow-sm p-4 border border-gray-100">
        <h3 class="text-lg font-semibold mb-2 text-azul-500">Company-wise Placements</h3>
        <apexchart type="pie" width="100%" :options="pie.options" :series="pie.series" />
      </div>
    </section>
  </template>
 