


<script setup>
// <ButtonC v-model="buttonState" :onActivate="() => {'here goes the function'}"> dodo</ButtonC>
import { defineProps } from 'vue';

defineProps({
  modelValue: {
    type: Boolean,
    required: true
  },
  onActivate: {
    type: Function,
    required: true
  }
});
</script>

<template>
  <button
    :disabled="!modelValue"
    @click="onActivate"
    class="custom-button"
  >
    <slot />
  </button>
</template>

<style scoped>
.custom-button {
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 4px;
  transition: background-color 0.3s ease, cursor 0.1s ease;
}


.custom-button:not(:disabled) {
  background-color: #28a745; 
  color: white;
  cursor: pointer;
}

.custom-button:not(:disabled):hover {
  background-color: #218838; 
}


.custom-button:disabled {
  background-color: #d3d3d3; 
  color: #6c757d; 
  cursor: not-allowed;
}
</style>