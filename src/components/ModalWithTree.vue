<template>
  <transition name="modal-fade" @after-enter="afterEnter">
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
  </transition>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits, defineExpose, onMounted } from 'vue'
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
  (event: 'select', folder: Folder): void // Эмитируем всю папку
}>()

const isVisible = ref(false)
const folders = ref<Folder[]>([])
let selectedFolder: Folder | null = null // Сохраняем выбранную папку

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
}

function closeModal() {
  isVisible.value = false
}

function selectFolder(folder: Folder) {
  selectedFolder = folder // Сохраняем выбранную папку
}

function handleSelect() {
  if (selectedFolder) {
    emit('select', selectedFolder) // Эмитируем всю папку
    closeModal()
  }
}

function afterEnter() {
  console.log('Модальное окно появилось')
}

defineExpose({
  showModal,
  closeModal,
})

onMounted(() => {
  fetchFolders()
})
</script>

<style scoped>
/* Стили для затемнения */
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
  opacity: 1; /* Плавное затемнение */
  transition: opacity 0.3s ease; /* Анимация для затемнения */
  margin-top: 0px;
}

/* Начальные стили для модального окна */
.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  width: 500px;
  max-width: 100%;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transform: scale(0.8); /* Начальный размер */
  transition: transform 0.3s ease; /* Анимация для масштабирования */
  z-index: 1100; /* Обеспечиваем, чтобы окно было выше */
}

/* Плавная анимация входа */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

/* Когда модальное окно появляется */
.modal-fade-enter, .modal-fade-leave-to /* .modal-fade-leave-active в <2.1.8 */ {
  opacity: 1;
  transform: scale(1); /* Увеличиваем до нормального размера */
}

/* Кнопки */
.modal-buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.modal-buttons button {
  padding: 10px 20px;
}

.folder-tree {
  margin-bottom: 10px;
}
</style>
