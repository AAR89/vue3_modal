<template>
  <div>
    <div class="buttons_container">
      <button @click="openModal">Открыть</button>

      <button @click="resetSelection">Сброс</button>
    </div>
    <!-- Сообщение с выбранным ID папки -->
    <div v-if="selectedFolderId">Вы выбрали папку с id: {{ selectedFolderId }}</div>

    <!-- Кнопка сброса -->

    <!-- Модальное окно -->
    <ModalWithTree title="Выберите папку" ref="modal" @select="handleFolderSelect" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ModalWithTree from './components/ModalWithTree.vue'

// Ссылка на модальное окно
const modal = ref<InstanceType<typeof ModalWithTree> | null>(null)

// Переменная для хранения ID выбранной папки
const selectedFolderId = ref<string | null>(null)

// Функция для открытия модального окна
function openModal() {
  modal.value?.showModal()
}

// Обработчик события select из модального окна
function handleFolderSelect(folderId: string) {
  selectedFolderId.value = folderId
  modal.value?.closeModal() // Закрыть модальное окно после выбора папки
}

// Функция сброса выбранного ID
function resetSelection() {
  selectedFolderId.value = null
}
</script>

<style scoped>
.buttons_container {
  display: flex;
  gap: 10px;
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
