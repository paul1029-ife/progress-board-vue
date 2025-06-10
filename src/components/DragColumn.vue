<template>
  <div class="w-82 h-fit min-h-32 bg-indigo-400 rounded-md text-white">
    <div class="border-b-3 flex justify-between items-center px-2 py-1 h-14 border-b-gray-600">
      <p class="text-xl">{{ header }}</p>
      <button class="bg-emerald-500 px-2 py-1 rounded-lg">+</button>
    </div>
    <ul class="pt-2">
      <li
        v-for="(item, index) in items"
        :key="index"
        class="px-4 py-7 hover:bg-indigo-500 transition-all cursor-grab rounded-lg flex justify-between"
      >
        {{ item }}
        <div class="flex gap-1 text-black items-center">
          <X class="w-5 h-5 cursor-pointer hover:text-emerald-500" />
          <Pen class="w-5 h-5 cursor-pointer hover:text-emerald-500" />
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { X, Pen } from 'lucide-vue-next'
defineProps({
  header: String,
  items: Array,
})
</script>
