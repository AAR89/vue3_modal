<template>
  <div>
    <button @click="showModal">Открыть модальное окно</button>
    <ModalComponent ref="modal">
      <h2>Это модальное окно!</h2>
      <p>Здесь может быть ваше содержимое.</p>
    </ModalComponent>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ModalComponent from './components/ModalComponent.vue'

// Типизация для ссылки на модальное окно
const modal = ref<InstanceType<typeof ModalComponent> | null>(null)

// Метод для открытия модального окна
function showModal(): void {
  modal.value?.showModal()
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
