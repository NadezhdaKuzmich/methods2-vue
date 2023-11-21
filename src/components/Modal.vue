<template>
  <div class="modal-container">
    <div class="modal-close" @click="closeModal"></div>
    <div class="modal">
      <div class="modal-content accent">
        <h3>{{ modalTitle }}</h3>
        <p>{{ modalMessage }}</p>
        <button @click="closeModal" class="btn-close">&#x2715;</button>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    modalTitle: String,
    modalMessage: String,
  },

  emits: ["close"],
  setup(props, { emit }) {
    function closeModal() {
      emit("close");
    }
    return {
      closeModal,
    };
  },
});
</script>

<style scoped>
.modal-container {
  position: fixed;
  overflow: hidden;
}
.modal-close {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
}
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  width: 40%;
  transform: translate(-50%, -50%);
}
.modal-content {
  width: 100%;
  background: #fff;
  border-radius: 8px;
  padding: 20px 40px;
}
.btn-close {
  position: absolute;
  top: 12px;
  right: 10px;
  line-height: 1;
  background: none;
  border: 0;
  padding: 2px 6px;
  cursor: pointer;
}
.btn-close:hover {
  color: #398877;
}
.accent {
  color: #4d644f;
}
</style>