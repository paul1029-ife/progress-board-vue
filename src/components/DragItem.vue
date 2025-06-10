<template>
  <li
    class="px-4 py-7 hover:bg-indigo-500 transition-all cursor-grab rounded-lg flex justify-between"
  >
    {{ item }}
    <div class="flex gap-1 text items-center">
      <X class="w-5 h-5 cursor-pointer hover:text-emerald-500" />
      <Pen class="w-5 h-5 cursor-pointer hover:text-emerald-500" />
    </div>
  </li>
</template>

<script setup>
import { X, Pen } from 'lucide-vue-next'
defineProps({
  item: String,
})
</script>
