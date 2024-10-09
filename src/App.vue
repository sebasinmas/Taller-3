<!--eslint-disable no-unused-vars -->
<script setup>
import { ref } from "vue";
import axios from 'axios';
const dataCountries = ref();
const dataAnimeRec = ref();
const dataAnime = ref();
const dataManga = ref();


const getApiCountries = async () => {
  try {
    dataCountries.value = await axios.get("https://countriesnow.space/api/v0.1/countries/population");

  } catch (e) {
    console.log(e);
  }
}

const getApiAnimeRec = async () => {
  try {
    dataAnimeRec.value = await axios.get("https://api.jikan.moe/v4/recommendations/anime");

  } catch (e) {
    console.log(e);
  }
}

const getApiAnime = async () => {
  try {
    dataAnime.value = await axios.get("https://api.jikan.moe/v4/random/anime");

  } catch (e) {
    console.log(e);
  }
}

const getApiManga = async () => {
  try {
    dataManga.value = await axios.get("https://api.jikan.moe/v4/random/manga");

  } catch (e) {
    console.log(e);
  }
}

</script>

<template>
  <header>
    <div class="paises">
      <button @click="getApiCountries">Conseguir países</button>
      <p>{{ dataCountries }}</p>

    </div>
    <div class="anime-recommendations">
      <button @click="getApiAnimeRec">Conseguir animes recomendados</button>
      <p>{{ dataAnimeRec }}</p>
    </div>
    <div class="anime">
      <button @click="getApiAnime">Conseguir animes</button>
      <p>{{ dataAnime }}</p>
    </div>
    <div class="manga">
      <button @click="getApiManga">Conseguir mangas</button>
      <p>{{ dataManga }}</p>
    </div>

  </header>
</template>

<style scoped></style>