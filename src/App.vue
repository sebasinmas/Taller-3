<!--eslint-disable no-unused-vars -->
<script setup>
import { ref, onMounted } from "vue";
import axios from 'axios';
import MangaComponent from "./components/MangaComponent.vue";
import CountryComponent from "./components/CountryComponent.vue";
import AnimeRecComponent from "./components/AnimeRecComponent.vue";
import AnimeComponent from "./components/AnimeComponent.vue";
const anime = ref([]);
const recom = ref([]);
const manga = ref([]);
const pais = ref([]);

const showManga = ref(false);
const showPais = ref(false);
const showRecom = ref(false);
const showAnime = ref(false);


//Funciones
const getRecom = async () => {
  try {
    const result = await axios.get("https://api.jikan.moe/v4/recommendations/anime");
    recom.value = result.data.data;
    showRecom.value = true;
    console.log("clicked")
  } catch (err) {
    console.log(err);
  }
}
const getPais = async () => {
  try {
    const result = await axios.get("https://api.jikan.moe/v4/random/manga");
    pais.value = result.data.data;
    showPais.value = true;
  } catch (err) {
    console.log(err);
  }
}
const getManga = async () => {
  try {
    const result = await axios.get("https://api.jikan.moe/v4/random/manga");
    manga.value = result.data.data;
    showManga.value = true;
  } catch (err) {
    console.log(err);
  }
}
const getAnime = async () => {
  try {
    const result = await axios.get("https://api.jikan.moe/v4/random/anime");
    anime.value = result.data.data;
    showAnime.value = true;
  } catch (err) {
    console.log(err);
  }
}


</script>

<template>
  <div class="container d-flex justify-content-right">
    <div class="recom">
      <button @click="getRecom">Mostrar recomendaciones de anime</button>
      <div v-if="showRecom">
        <AnimeRecComponent :recom="recom"></AnimeRecComponent>
      </div>
    </div>
    <div class="anime">
      <button @click="getAnime">Mostrar anime</button>
      <div v-if="showAnime">
        <AnimeComponent :anime="anime"></AnimeComponent>
      </div>
    </div>
    <div class="manga">
      <button @click="getManga">Mostrar manga</button>
      <div v-if="showManga">
        <MangaComponent :manga="manga"></MangaComponent>
      </div>
    </div>
  </div>
</template>

<style scoped></style>