<template>
  <div v-if="isVisible" class="modal-overlay" @click.self="closeModal">
    <div class="modal-content">
      <h2>{{ title }}</h2>
      <div class="folder-tree">
        <FolderTree :folders="folders" @select-folder="selectFolder" />
      </div>
      <div class="modal-buttons">
        <button @click="handleSelect">Ок</button>
        <button @click="closeModal">Закрыть</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue'
import axios from 'axios'
import FolderTree from './FolderTree.vue'

interface Folder {
  id: string
  name: string
  children: Folder[]
}

defineProps<{
  title: string
}>()

const emit = defineEmits<{
  (event: 'select', folderId: string): void
}>()

const isVisible = ref(false)
const folders = ref<Folder[]>([])
const selectedFolderId = ref<string | null>(null)

const fetchFolders = async () => {
  try {
    const response = await axios.get('https://190c996e07b108af.mokky.dev/mockFolders')
    folders.value = response.data
  } catch (error) {
    console.error('Ошибка при загрузке данных папок:', error)
  }
}

function showModal() {
  isVisible.value = true
  fetchFolders()
}

function closeModal() {
  isVisible.value = false
}

function selectFolder(folderId: string) {
  selectedFolderId.value = folderId
}

function handleSelect() {
  console.log('handleSelect')
  if (selectedFolderId.value) {
    emit('select', selectedFolderId.value)
    closeModal()
  }
}

defineExpose({
  showModal,
  closeModal,
})
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  width: 500px;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.folder-tree {
  max-height: 300px;
  overflow-y: auto;
  margin-bottom: 20px;
}

.modal-buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.modal-buttons button {
  padding: 10px 20px;
}
</style>
