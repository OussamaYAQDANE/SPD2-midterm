<template>
  <div class="MainPage">
    <div class="search-div"> <input id="search" type="text" v-model="query"
        placeholder="Chercher un livre par titre ou par auteur ici">

      <DropDown class="drop-down" :options="[ 'tout','disponible', 'emprunté']" placeholder="filtrer" v-model="dispo" />
    </div>
    <LibraryC class="Library"
      :livres="livres.filter(livre => (livre.titre.toLowerCase().includes(query.toLowerCase()) || livre.auteur.toLowerCase().includes(query.toLowerCase())) && (dispo == 'tout' || (dispo == 'disponible' && livre.disponible == true) || (dispo == 'emprunté' && livre.disponible == false)))  " />
    <ModalVue v-model="modalOpen">
      <div class="modal-content">
        <img class="hh" :src="modalLivre.image" alt="Image du livre">
        <span>Titre: {{ modalLivre.titre }}</span>
        <span>Auteur: {{ modalLivre.auteur }}</span>
        <span>Année de publication: {{ modalLivre.annee }}</span>
        <span>Résumé: {{ modalLivre.resume }}</span>

        <span>Status: <span :style="{ color: modalLivre.disponible ? 'green' : 'red' }">{{ modalLivre.disponible ?
            'Disponible' : 'Emprunté' }}</span></span>
      </div>
    </ModalVue>
  </div>

</template>

<script setup>
import { ref } from 'vue';
import LibraryC from '@/components/LibraryC.vue';
import DropDown from '@/components/DropDown.vue';
import ModalVue from '@/components/ModalVue.vue';
import { provide } from 'vue';
const query = ref('');

const dispo = ref('tout')
const livres = ref([]);
const modalOpen = ref(false);
const modalLivre = ref({});

function openModal(livre){
  modalLivre.value = livre;
  modalOpen.value = true;
}
provide('openModal', openModal);

fetch("http://localhost:3000/livres")
.then(response=>response.json())
.then(data=>{livres.value = data});

</script>

<style scoped>
.MainPage{
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 100%;
  background-color: #242424;
  height: 100vh;
  padding: 20px;
  justify-content: center;
}

.Library{
  width: 40%;
  background-color: rgb(45, 45, 45);

}
.modal-content{
  display: flex;
  flex-direction: column;
  margin-top: 15px;
}
.search-div{
  display: flex;
 
  width: 40%;
  margin: 5px;
  align-items: center;
  
}
.drop-down{
  width: 30%;
  border-radius: 10px;
  height: 50px;
}
#search{
  padding: 10px;
  outline: none;
  border-radius: 10px;
  color: black;
  width: 70%;
  height: 50px;
}
span{
  color: black;
  margin-bottom: 12px;
}
.hh{
  justify-self: center;
  align-self: center;
  margin-bottom: 20px;
  color: black;
  width: 150px

}
</style>