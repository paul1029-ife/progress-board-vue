<script setup>
import Navbar from './components/Navbar.vue'
import DragColumn from './components/DragColumn.vue'

const items = ['Task 1', 'Task 2', 'Task 3', 'Task 4', 'Task 5']
</script>

<template>
  <div class="bg-gray-300 min-h-screen pt-6 flex flex-col gap-8">
    <Navbar />
    <div class="flex items-center justify-center gap-5">
      <DragColumn header="Table 1" :items="items" />
      <DragColumn header="Table 1" :items="items" />
      <DragColumn header="Table 1" :items="items" />
    </div>
  </div>
</template>
