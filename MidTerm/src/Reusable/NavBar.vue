<script setup>

{/* <NavBar :fixed="true">
    <template #brand>
      <a href="/">My App</a>
    </template>
    <template #menu>
      <a href="/about">About</a>
      <a href="/contact">Contact</a>
      <a href="/profile">Profile</a>
    </template>
  </NavBar> */}

import { computed, defineProps } from 'vue';

const props = defineProps({
  fixed: {
    type: Boolean,
    default: false
  }
});

const navbarClass = computed(() => ({
  'navbar': true,
  'navbar-fixed': props.fixed
}));
</script>

<template>
  <nav :class="navbarClass">
    <div class="navbar-brand">
      <slot name="brand"></slot>
    </div>
    <div class="navbar-menu">
      <slot name="menu"></slot>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  background-color: #333;
  color: white;
  padding: 10px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar-fixed {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
}

.navbar-brand {
  font-size: 1.5rem;
}

.navbar-brand a {
  color: white;
  text-decoration: none;
}

.navbar-menu {
  display: flex;
  gap: 15px;
}

.navbar-menu > * {
  color: white;
  text-decoration: none;
  padding: 5px 10px;
  border-radius: 4px;
}

.navbar-menu > *:hover {
  background-color: #555;
}
</style>