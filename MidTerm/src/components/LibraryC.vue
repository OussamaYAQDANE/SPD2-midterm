<template>
  <div class="scrollable-div">
    <LivreTile class="Tile" v-for="livre in livres" :key="livre.id" :livre="livre" />

  </div>
</template>

<script setup>
import { defineProps } from 'vue';
import LivreTile from './LivreTile.vue';

defineProps({
  livres: Array
})


</script>

<style scoped>


.scrollable-div {
  overflow: auto;
  position: relative;
  scrollbar-color: #fff rgb(45, 45, 45);
  scrollbar-width: thin;
  height: 80vh;
}

.Tile{
  border-bottom: 1px solid #fff;
}
</style>