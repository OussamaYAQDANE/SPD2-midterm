<template>

    <div class="card" @click="openModal(livre)"><span style="">{{ livre.titre }}</span> <span :style="{ color: livre.disponible ? 'lightgreen' : 'red' }"> {{ livre.disponible? 'disponible': 'emprunté' }} </span> </div>
</template>

<script setup>
import { defineProps, ref, onMounted, inject } from 'vue';

const openModal = inject('openModal');

const img = ref('');

const props = defineProps({
  livre: Object
});

onMounted(() => {
  img.value = `http://localhost:3000${props.livre.image}`;
});

</script>

<style scoped>
.card{
    height: 50px;
    
    background-color: rgb(60,60,60);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px;
}
</style>