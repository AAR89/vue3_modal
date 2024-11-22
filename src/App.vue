<template>
  <div>
    <button @click="openModal">Открыть дерево папок</button>
    <ModalWithTree title="Выберите папку" ref="modal" @select="handleFolderSelect" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ModalWithTree from './components/ModalWithTree.vue'

const modal = ref<InstanceType<typeof ModalWithTree> | null>(null)

function openModal() {
  modal.value?.showModal()
}

// Обработчик события select из модального окна
function handleFolderSelect(folderId: string) {
  console.log('Вы выбрали папку с id:', folderId)
}
</script>

<style scoped>
button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
}
</style>
