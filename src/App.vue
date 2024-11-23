<template>
  <div>
    <div class="buttons_container">
      <button v-if="!selectedFolder" @click="openModal">Открыть</button>

      <!-- Кнопка для сброса выбора папки -->
      <button v-if="selectedFolder" @click="resetSelection">Сброс</button>
    </div>

    <!-- Сообщение с названием выбранной папки -->
    <div v-if="selectedFolder">Вы выбрали папку с названием: {{ selectedFolder.name }}</div>

    <!-- Модальное окно -->
    <ModalWithTree title="Выберите папку" ref="modal" @select="handleFolderSelect" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ModalWithTree from './components/ModalWithTree.vue'

// Ссылка на модальное окно
const modal = ref<InstanceType<typeof ModalWithTree> | null>(null)

// Переменная для хранения выбранной папки
const selectedFolder = ref<{ id: string; name: string } | null>(null)

// Функция для открытия модального окна
function openModal() {
  modal.value?.showModal()
}

// Обработчик события select из модального окна
function handleFolderSelect(folder: { id: string; name: string }) {
  selectedFolder.value = folder // Обновляем выбранную папку
  modal.value?.closeModal() // Закрываем модальное окно после выбора
}

// Функция сброса выбранной папки
function resetSelection() {
  selectedFolder.value = null
}
</script>

<style scoped>
.buttons_container {
  width: 280px;
  display: flex;
  gap: 10px;
  justify-content: center;
}

button {
  width: 100px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  margin: 5px 0;
}

div {
  margin-top: 20px;
}
</style>
