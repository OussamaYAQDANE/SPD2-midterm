<script setup>
import { ref, defineProps } from 'vue';

// Define the props for the component
const props = defineProps({
  tabs: {
    type: Array,
    required: true,
    validator: (value) => value.every(tab => typeof tab.label === 'string' && typeof tab.slotName === 'string')
  }
});

// Reactive state to track the active tab (index-based)
const activeTab = ref(0);
</script>

<template>
  <div class="tab-container">
    <!-- Tab Bar -->
    <div class="tab-bar">
      <button
        v-for="(tab, index) in props.tabs"
        :key="index"
        @click="activeTab = index"
        :class="{ 'active': activeTab === index }"
      >
        {{ tab.label }}
      </button>
    </div>

    <!-- Tab Content -->
    <div class="tab-content">
      <transition name="fade">
        <div :key="activeTab">
          <slot :name="props.tabs[activeTab].slotName"></slot>
        </div>
      </transition>
    </div>
  </div>
</template>

<style scoped>
.tab-container {
  width: 100%;
}

.tab-bar {
  display: flex;
  background-color: #f0f0f0;
}

.tab-bar button {
  padding: 10px 20px;
  background: none;
  border: none;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.2s;
}

.tab-bar button:hover {
  background-color: #e0e0e0;
}

.tab-bar button.active {
  background-color: white;
  border-bottom: 2px solid #28a745;
}

.tab-content {
  padding: 20px;
  background-color: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>