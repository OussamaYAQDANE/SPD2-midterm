<script setup>
import { ref, computed, defineProps,  } from 'vue';

// <InputC label="label" errorMessage="not this broo" v-model="input" :validator="(x)=>{return x.includes('.')}" />

const props = defineProps({
  modelValue: {
    type: String,
    required: true
  },
  validator: {
    type: Function,
    required: true
  },
  errorMessage: {
    type: String,
    required: true
  },
  label: {
    type: String,
    default: ''
  }
});


const touched = ref(false);

const isValid = computed(() => { return props.validator(props.modelValue)});


</script>

<template>
  <div class="input-container">
    
    <label v-if="label" class="input-label">{{ label }}</label>
  
    <input
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value); console.log(isValid, modelValue);"
      @blur="touched=true"
      :class="{ 'input-error': !isValid && touched }"
      class="input-field"
    />
    
    <div v-if="!isValid && touched" class="error-message">{{ errorMessage }}</div>
  </div>
</template>

<style scoped>
.input-container {
  margin-bottom: 16px;
}

.input-label {
  display: block;
  font-size: 14px;
  color: #333;
  margin-bottom: 4px;
}

.input-field {
  padding: 8px 12px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 100%;
  box-sizing: border-box;
  transition: border-color 0.3s ease;
}

.input-field:focus {
  outline: none;
  border-color: #28a745; 
  box-shadow: 0 0 5px rgba(40, 167, 69, 0.5);
}

.input-field.input-error {
  border-color: red; 
}

.error-message {
  color: red;
  font-size: 12px;
  margin-top: 4px;
}
</style>