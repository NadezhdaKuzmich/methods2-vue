<template>
  <div class="container" :class="{ hidden: isModalOpen }">
    <h1>Fundamentals of working with components: props, emit</h1>
    <div class="examples">
      <div class="example">
        <div class="modal-form">
          <h2>Emit:</h2>
          <label for="modalTitle">Title:</label>
          <input
            type="text"
            id="modalTitle"
            v-model="modalTitle"
            placeholder="Create custom title" />
          <label for="modalMessage">Message:</label>
          <input
            type="text"
            id="modalMessage"
            v-model="modalMessage"
            placeholder="Create custom message" />
          <button class="btn" @click="showModal">Show Modal Window</button>
          <p v-if="isError" class="error">
            First you need to create a title and message for your modal window.
          </p>
          <Modal
            v-if="isModalOpen"
            :modal-title="modalTitle"
            :modal-message="modalMessage"
            @close="closeModal" />
        </div>
      </div>
      <div class="example counter-container">
        <h2>Input <span class="small">(parent component)</span></h2>
        <input type="number" v-model="counter" />
        <Counter :counter="counter" />
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";
import Counter from "./components/Counter.vue";
import Modal from "./components/Modal.vue";

export default defineComponent({
  components: { Counter, Modal },
  setup() {
    const counter = ref(0);
    const isModalOpen = ref(false);
    const modalTitle = ref("");
    const modalMessage = ref("");
    const isError = ref(false);

    function showModal() {
      if (modalTitle.value && modalMessage.value) {
        isModalOpen.value = true;
      } else {
        isError.value = true;
      }
    }

    function closeModal() {
      isModalOpen.value = false;
      isError.value = false;
      modalTitle.value = "";
      modalMessage.value = "";
    }

    return {
      counter,
      isModalOpen,
      modalTitle,
      modalMessage,
      isError,
      showModal,
      closeModal,
    };
  },
});
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  font-size: 18px;
  color: #233525;
  text-align: center;
}

.container {
  max-width: 1000px;
  padding: 20px 20px 40px;
  margin: auto;
}

.examples {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 40px 0 0;
  gap: 20px;
}

.example {
  width: 100%;
  max-width: 500px;
  background: #dbede0;
  box-shadow: 1px 2px 8px #afb9af;
  border-radius: 8px;
  margin: auto;
  padding: 20px 20px 40px;
}

.small {
  font-size: 14px;
  font-weight: 300;
  color: #398877;
}

.counter-container input {
  padding: 6px;
}

.modal-form {
  max-width: 400px;
  display: flex;
  flex-direction: column;
  text-align: left;
  margin: 0 auto 20px;
  gap: 10px;
}

input {
  font-size: 16px;
  color: #233525;
  border: 1px solid #398877;
  border-radius: 5px;
  padding: 12px 10px;
}

.btn {
  font-size: 16px;
  font-weight: 600;
  color: #233525;
  background: #f9f9f9;
  border: 2px solid #398877;
  border-radius: 6px;
  padding: 10px 20px;
  margin: 20px 0 0;
  cursor: pointer;
  transition: all 0.5s ease-in-out;
}

.btn:hover {
  color: #fff;
  background: #398877;
}

.error {
  font-size: 14px;
  color: #4b7e89;
  text-align: center;
  margin: 0;
}
</style>