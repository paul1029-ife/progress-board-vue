<script setup lang="ts">
import DragColumn from '@/components/DragColumn.vue'
import { ref } from 'vue'

interface Columns {
  [key: string]: string[]
}

const columns = ref<Columns>({
  'To Do': ['Task 1', 'Task 2', 'Task 3'],
  'In Progress': ['Task 4'],
  Done: ['Task 5'],
})

interface DropEvent {
  item: string
  columnId: string
}

interface EditEvent {
  oldItem: string
  newItem: string
  columnId: string
}

interface DeleteEvent {
  item: string
  columnId: string
}

const handleItemDrop = ({ item, columnId }: DropEvent) => {
  Object.keys(columns.value).forEach((key) => {
    columns.value[key] = columns.value[key].filter((i) => i !== item)
  })

  if (columns.value[columnId]) {
    columns.value[columnId].push(item)
  } else {
    console.warn(`Column "${columnId}" does not exist.`)
  }
}

const handleItemEdit = ({ oldItem, newItem, columnId }: EditEvent) => {
  if (columns.value[columnId]) {
    const index = columns.value[columnId].indexOf(oldItem)
    if (index !== -1) {
      columns.value[columnId][index] = newItem
    }
  }
}

const handleItemDelete = ({ item, columnId }: DeleteEvent) => {
  if (columns.value[columnId]) {
    columns.value[columnId] = columns.value[columnId].filter((i) => i !== item)
  }
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
      @item-edit="handleItemEdit"
      @item-delete="handleItemDelete"
    />
  </div>
</template>
