<template>
  <li
    class="px-4 py-7 bg-indigo-500 transition-all cursor-grab rounded-lg flex justify-between mx-2"
    draggable="true"
    @dragstart="onDragStart"
    @dragend="onDragEnd"
  >
    {{ item }}
    <div class="flex gap-1 text items-center">
      <X class="w-5 h-5 cursor-pointer hover:text-emerald-500" />
      <Pen class="w-5 h-5 cursor-pointer hover:text-emerald-500" />
    </div>
  </li>
</template>

<script setup lang="ts">
import { X, Pen } from 'lucide-vue-next'

const props = defineProps({
  item: String,
})

const emit = defineEmits(['dragstart', 'dragend'])

const onDragStart = (e: DragEvent) => {
  if (e.dataTransfer) {
    e.dataTransfer.effectAllowed = 'move'
    e.dataTransfer.setData('text/plain', props.item || '')
  }
  emit('dragstart', e)
}

const onDragEnd = (e: DragEvent) => {
  emit('dragend', e)
}
</script>
