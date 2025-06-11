<script setup>
import DragColumn from '@/components/DragColumn.vue'
import { ref } from 'vue'
const columns = ref({
  'To Do': ['Task 1', 'Task 2', 'Task 3'],
  'In Progress': ['Task 4'],
  Done: ['Task 5'],
})

const handleItemDrop = ({ item, columnId }) => {
  Object.keys(columns.value).forEach((key) => {
    columns.value[key] = columns.value[key].filter((i) => i !== item)
  })

  // Add item to the target column
  columns.value[columnId].push(item)
}
</script>
<template>
  <div class="flex items-start justify-center gap-5">
    <DragColumn
      v-for="(items, header) in columns"
      :key="header"
      :header="header"
      :items="items"
      @item-drop="handleItemDrop"
    />
  </div>
</template>
