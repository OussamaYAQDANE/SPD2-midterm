<script setup>


import { defineProps, defineEmits } from 'vue';

defineProps({
  options: {
    type: Array,
    required: true
  },
  modelValue: {
    type: String,
    default: ''
  },

  placeholder: {
    type: String,
    default: ''
  }
});

defineEmits(['update:modelValue']);
</script>

<template>
  <select
    :value="modelValue"
    @change="$emit('update:modelValue', $event.target.value);"
    
    class="custom-select"
  >
    <option v-if="placeholder" value="" disabled :selected="modelValue === ''" >{{ placeholder }}</option>
    <option v-for="option in options" :key="option" :value="option" >{{ option }}</option>
  </select>
</template>

<style scoped>
*{
  color: black
}
.custom-select {
  padding: 8px 12px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: white;
  cursor: pointer;
  color: black;
  transition: border-color 0.3s ease;
  outline: none;
}




</style>