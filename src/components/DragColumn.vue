<template>
  <div class="w-82 h-fit min-h-32 bg-indigo-400 rounded-md text-white">
    <div class="border-b-3 flex justify-between items-center px-2 py-1 h-14 border-b-gray-600">
      <p class="text-xl">{{ header }}</p>
      <button class="bg-emerald-500 px-2 py-1 rounded-lg cursor-pointer">+</button>
    </div>
    <ul class="pt-2">
      <DragItem v-for="(item, index) in items" :item="item" :key="index" />
    </ul>
  </div>
</template>

<script setup>
import DragItem from './DragItem.vue'
defineProps({
  header: String,
  items: Array,
})
</script>
