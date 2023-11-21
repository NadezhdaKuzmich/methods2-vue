<template>
  <div class="counter">
    <h2>Counter <span class="small">(child component)</span></h2>
    <p class="count">{{ counter }}</p>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    counter: Number,
  },
  setup() {
    return {};
  },
});
</script>

<style scoped>
.count {
  font-size: 24px;
  font-weight: 600;
  color: #398877;
  margin-bottom: 0;
}
</style>