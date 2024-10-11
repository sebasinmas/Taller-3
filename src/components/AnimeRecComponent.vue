<script setup>
import { defineProps } from 'vue'
defineProps({
  recom: {
    type: Object,
    Required: true
  }
})
</script>
<template>
  <div class="container" v-if="recom">
    <!--  Esto es que se cargó bien el JSON   -->
    <div
      class="card mx-auto"
      style="max-width: min-content; margin-bottom: 40px"
      v-for="(catalogo, index) in recom"
      :key="index"
    >
      <!-- Estoy iterando sobre la primera parte del Json que son como catalogos de tal numero a tal numero-->
      <h1>Recomendación de {{ catalogo.user.username }}</h1>
      <div v-for="(entry, index) in catalogo.entry" v-bind:key="index">
        <!-- Estoy iterando sobre los animes en esos catálogos -->
        <a class="link-dark" :href="entry.url">
          <h1>{{ entry.title }}</h1>
        </a>
        <img class="" :src="entry.images.jpg.image_url" />
      </div>
      <p>{{ catalogo.content }}</p>
    </div>
  </div>
  <div v-else>
    <h1>Cargando api...</h1>
  </div>
</template>
<style scoped></style>
