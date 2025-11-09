<template>
    <div class="bg-white rounded-2xl p-4 shadow-sm border border-gray-100">
      <p class="text-sm text-gray-500">{{ label }}</p>
      <h2 class="text-2xl font-bold text-azul-500">{{ value }}</h2>
    </div>
  </template>
  
  <script setup>
  defineProps({
    label: String,
    value: [String, Number],
  })
  </script>
  