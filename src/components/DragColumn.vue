<template>
  <div
    class="w-82 h-fit min-h-32 bg-indigo-400 rounded-md text-white"
    @dragover.prevent
    @drop="onDrop"
  >
    <div class="border-b-3 flex justify-between items-center px-2 py-1 h-14 border-b-gray-600">
      <p class="text-xl">{{ header }}</p>
      <button class="bg-emerald-500 px-2 py-1 rounded-lg cursor-pointer">+</button>
    </div>
    <ul class="pt-2">
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
