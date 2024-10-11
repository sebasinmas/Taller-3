<!--eslint-disable no-unused-vars -->
<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import MangaComponent from './components/MangaComponent.vue'
import CountryComponent from './components/CountryComponent.vue'
import AnimeRecComponent from './components/AnimeRecComponent.vue'
import AnimeComponent from './components/AnimeComponent.vue'
const anime = ref([])
const recom = ref([])
const manga = ref([])
const pais = ref([])

const showManga = ref(false)
const showPais = ref(false)
const showRecom = ref(false)
const showAnime = ref(false)

//Funciones
const getRecom = async () => {
  toggle()
  try {
    const result = await axios.get('https://api.jikan.moe/v4/recommendations/anime')
    recom.value = result.data.data
    showRecom.value = true
    console.log('clicked')
  } catch (err) {
    console.log(err)
  }
}
const getPais = async () => {
  toggle2();
  try {
    const result = await axios.get('https://countriesnow.space/api/v0.1/countries/population')
    pais.value = result.data.data
    showPais.value = true
  } catch (err) {
    console.log(err)
  }
}
const getManga = async () => {
  try {
    const result = await axios.get('https://api.jikan.moe/v4/random/manga')
    manga.value = result.data.data
    showManga.value = true
  } catch (err) {
    console.log(err)
  }
}
const getAnime = async () => {
  try {
    const result = await axios.get('https://api.jikan.moe/v4/random/anime')
    anime.value = result.data.data
    showAnime.value = true
  } catch (err) {
    console.log(err)
  }
}

// Boton
// Definir el estado inicial como 'false'
const isOn = ref(true)
const isOn2 = ref(true)
// Función para alternar el estado del botón
const toggle = () => {
  isOn.value = !isOn.value
}
const toggle2 = () => {
  showPais.value = !showPais.value
}
</script>

<template>
  <div class="container mx-auto my-1 py-2 bg-light" style="width: 90vw; border-radius: 30px">
    <div class="row justify-content-center">
      <div class="recom col text-center">
        <button type="button" class="btn btn-dark" @click="getRecom">
          {{ isOn ? 'Mostrar recomendaciones de anime' : 'Ocultar recomendaciones de anime' }}
        </button>
        <div :hidden="isOn" v-if="showRecom" class="justify-content-center">
          <AnimeRecComponent :recom="recom"></AnimeRecComponent>
        </div>
      </div>
      <div class="anime col text-center">
        <button type="button" class="btn btn-dark" @click="getAnime">
          {{ !showAnime ? 'Mostrar Anime' : 'Actualizar Anime' }}
        </button>
        <div v-if="showAnime">
          <button type="button" class="mt-2 btn btn-dark" @click="showAnime = !showAnime">
            Ocultar anime
          </button>

          <AnimeComponent :hidden="showAnime" :anime="anime"></AnimeComponent>
        </div>
      </div>
      <div class="manga col text-center">
        <button type="button" class="btn btn-dark" @click="getManga">
          {{ !showManga ? 'Mostrar Manga' : 'Actualizar Manga' }}
        </button>
        <div v-if="showManga">
          <button type="button" class="mt-2 btn btn-dark" @click="showManga = !showManga">
            Ocultar manga
          </button>
          <MangaComponent :hidden="!showManga" :manga="manga"></MangaComponent>
        </div>
      </div>
    </div>
    <div class="container my-5 mx-auto">
      <div class="paises text-center">
        <button type="button" class="btn btn-dark" @click="getPais">
          {{ !showPais ? 'Mostrar países' : 'Ocultar países' }}
        </button>
        <div v-if="showPais" class="justify-content-center">
          <CountryComponent :hidden="!showPais" :pais="pais"></CountryComponent>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
