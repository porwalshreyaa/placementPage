<script setup>
import { ref, computed, onMounted } from 'vue'
import PrimaryButton from '@/components/PrimaryButton.vue'
import StatsCard from '@/components/StatsCard.vue'
import ChartsSection from '@/components/ChartsSection.vue'

const searchQuery = ref('')
const filter = ref({ year: '' })
const years = [2023, 2024, 2025]

const stats = ref([
  { label: 'Total Candidates', value: 250 },
  { label: 'Placed', value: 180 },
  { label: 'Placement Rate', value: '72%' },
  { label: 'Top Recruiter', value: 'Infosys' },
])

const placements = ref([
  { id: 1, name: 'Aditi Sharma', department: 'CSE', company: 'TCS', designation: 'Engineer', package: 6, status: 'Placed' },
  { id: 2, name: 'Rahul Mehta', department: 'ECE', company: 'Wipro', designation: 'Analyst', package: 5, status: 'Placed' },
  { id: 3, name: 'Neha Verma', department: 'IT', company: 'IBM', designation: 'Developer', package: 7, status: 'Placed' },
  { id: 4, name: 'Arjun Singh', department: 'ME', company: '-', designation: '-', package: 0, status: 'Pending' },
])

const filteredPlacements = computed(() =>
  placements.value.filter(p =>
    p.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
    p.company.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
)

const openCandidate = (row) => {
  console.log('Candidate clicked:', row)
}

const fetchPlacements = () => {
  console.log('Fetching placements for year:', filter.value.year)
}

onMounted(() => {
  // initial load
})
</script>


<template>
  
    <div class="p-6 space-y-8 bg-gray-50 min-h-screen">
      <!-- Header -->
      <header class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
        <div class="flex items-center gap-3">
          <!-- <img src="@/assets/logo.svg" alt="Company Logo" class="h-8" /> -->
          <h1 class="text-3xl font-semibold text-azul-500">Placements Overview</h1>
        </div>
        
  
        <div class="flex gap-3 items-center">
          <input
            v-model="searchQuery"
            type="text"
            placeholder="Search candidates or companies..."
            class="px-3 py-2 rounded-xl border border-gray-300 focus:ring focus:ring-azul-300"
          />
          <select v-model="filter.year" class="px-3 py-2 rounded-xl border border-gray-300">
            <option value="">All Years</option>
            <option v-for="y in years" :key="y" :value="y">{{ y }}</option>
          </select>
          <PrimaryButton @click="fetchPlacements">Apply</PrimaryButton>
        </div>
      </header>
  
      <!-- Stats -->
      <section class="grid gap-4 sm:grid-cols-2 lg:grid-cols-4">
        <StatsCard
          v-for="(stat, i) in stats"
          :key="i"
          :label="stat.label"
          :value="stat.value"
        />
      </section>
  
      <!-- Charts -->
      <ChartsSection />
  
      <!-- Placements Table -->
      <section class="bg-white rounded-2xl shadow-sm p-4 border border-gray-100">
        <h3 class="text-lg font-semibold mb-4 text-azul-500">Placements Data</h3>
  
        <table class="min-w-full text-sm text-left">
          <thead>
            <tr class="border-b bg-azul-50 text-azul-700">
              <th class="px-3 py-2">Candidate</th>
              <th class="px-3 py-2">Department</th>
              <th class="px-3 py-2">Company</th>
              <th class="px-3 py-2">Designation</th>
              <th class="px-3 py-2">Package</th>
              <th class="px-3 py-2">Status</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="row in filteredPlacements"
              :key="row.id"
              class="border-b hover:bg-azul-50 cursor-pointer"
              @click="openCandidate(row)"
            >
              <td class="px-3 py-2">{{ row.name }}</td>
              <td class="px-3 py-2">{{ row.department }}</td>
              <td class="px-3 py-2">{{ row.company }}</td>
              <td class="px-3 py-2">{{ row.designation }}</td>
              <td class="px-3 py-2">{{ row.package }} LPA</td>
              <td class="px-3 py-2">
                <span
                  class="px-2 py-1 rounded-full text-xs"
                  :class="row.status === 'Placed'
                    ? 'bg-azul-100 text-azul-700'
                    : 'bg-yellow-100 text-yellow-700'"
                >
                  {{ row.status }}
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </section>
    </div>
  </template>
  
