<template>
  <div
    class="w-82 h-fit min-h-32 bg-indigo-300 rounded-md text-white pb-2"
    @dragover.prevent
    @drop="onDrop"
  >
    <div class="border-b-1 flex justify-between items-center px-2 py-1 h-14 border-b-gray-300">
      <p class="text-lg">{{ header }}</p>
      <div class="flex gap-1">
        <button class="bg-emerald-500 px-2 py-1 rounded-lg cursor-pointer">
          <PlusIcon class="w-4 h-4" />
        </button>
        <button class="hover:opacity-70 cursor-pointer">
          <ChevronDown class="w-4 h-4" />
        </button>
      </div>
    </div>
    <ul class="pt-2 space-y-3">
      <DragItem
        v-for="(item, index) in items"
        :item="item"
        :key="index"
        @dragstart="onDragStart"
        @dragend="onDragEnd"
      />
    </ul>
  </div>
</template>

<script setup lang="ts">
import DragItem from './DragItem.vue'
import { PlusIcon } from 'lucide-vue-next'
import { ChevronDown } from 'lucide-vue-next'

const props = defineProps({
  header: String,
  items: Array as () => string[],
})

const emit = defineEmits(['itemDrop', 'itemDragStart', 'itemDragEnd'])

const onDrop = (e: DragEvent) => {
  e.preventDefault()
  const item = e.dataTransfer?.getData('text/plain')
  if (item) {
    emit('itemDrop', { item, columnId: props.header })
  }
}

const onDragStart = (e: DragEvent) => {
  emit('itemDragStart', { event: e, columnId: props.header })
}

const onDragEnd = (e: DragEvent) => {
  emit('itemDragEnd', { event: e, columnId: props.header })
}
</script>
