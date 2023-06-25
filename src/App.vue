<script setup>
    import { ref } from 'vue';
    import Modal from './components/Modal.vue';
    import './assets/style.css';

    const isModalOpen = ref(false);
    const isButtonHidden = ref(false);

    function openModal() {
        isModalOpen.value = true;
        isButtonHidden.value = true;
    }

    function closeModal() {
        isModalOpen.value = false;
        isButtonHidden.value = false;
    }
</script>

<template>
    <main class="container">
      <button v-if="!isModalOpen && !isButtonHidden" class="center-button" @click="openModal">Открыть меню</button>
  
      <Modal v-if="isModalOpen" @closeModal="closeModal" />

    </main>
</template>


