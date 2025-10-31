<template>
  <li
    class="px-4 py-7 bg-indigo-500 transition-all rounded-lg flex justify-between mx-2"
    :class="{ 'cursor-grab': !isEditing, 'cursor-default': isEditing }"
    :draggable="!isEditing"
    @dragstart="onDragStart"
    @dragend="onDragEnd"
  >
    <input
      v-if="isEditing"
      ref="editInput"
      v-model="editValue"
      class="bg-indigo-400 text-white outline-none border-b-2 border-white flex-1 mr-2"
      @keyup.enter="saveEdit"
      @keyup.esc="cancelEdit"
      @blur="saveEdit"
    />
    <span v-else>{{ item }}</span>

    <div class="flex gap-1 items-center">
      <X
        class="w-5 h-5 cursor-pointer hover:text-red-400 transition-colors"
        @click="handleDelete"
      />
      <Pen
        v-if="!isEditing"
        class="w-5 h-5 cursor-pointer hover:text-emerald-500 transition-colors"
        @click="startEdit"
      />
    </div>
  </li>
</template>

<script setup lang="ts">
import { ref, nextTick } from 'vue'
import { X, Pen } from 'lucide-vue-next'

const props = defineProps({
  item: String,
})

const emit = defineEmits(['dragstart', 'dragend', 'edit', 'delete'])

const isEditing = ref(false)
const editValue = ref('')
const editInput = ref<HTMLInputElement | null>(null)

const onDragStart = (e: DragEvent) => {
  if (isEditing.value) return
  if (e.dataTransfer) {
    e.dataTransfer.effectAllowed = 'move'
    e.dataTransfer.setData('text/plain', props.item || '')
  }
  emit('dragstart', e)
}

const onDragEnd = (e: DragEvent) => {
  emit('dragend', e)
}

const startEdit = async () => {
  isEditing.value = true
  editValue.value = props.item || ''
  await nextTick()
  editInput.value?.focus()
  editInput.value?.select()
}

const saveEdit = () => {
  if (editValue.value.trim() && editValue.value !== props.item) {
    emit('edit', { oldItem: props.item, newItem: editValue.value.trim() })
  }
  isEditing.value = false
}

const cancelEdit = () => {
  isEditing.value = false
  editValue.value = ''
}

const handleDelete = () => {
  emit('delete', props.item)
}
</script>
