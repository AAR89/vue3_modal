<template>
  <div>
    <button @click="showModal">Открыть модальное окно</button>
    <Modal ref="modal">
      <h2>Это модальное окно!</h2>
      <p>Здесь может быть ваше содержимое.</p>
    </Modal>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Modal from './components/ModalComponent.vue'

const modal = ref(null)

function showModal() {
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
