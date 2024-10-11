<script setup>
import { defineProps } from 'vue'
defineProps({
  pais: {
    type: Object,
    Required: true
  }
})


</script>
<template>
  <div class="container my-2" v-if="pais">
    <div v-for="(paises, index) in pais" :key="index">
      <div style="font-size: 2rem;"><strong>{{ paises.country }}</strong> Código: {{ paises.code }}</div>
      <div v-for="(datos, index) in paises.populationCounts" :key="index">
        En el año: <strong>{{ datos.year }}</strong> <br>
        habían: <strong>{{ datos.value }} </strong> habitantes<br>
        <hr>
      </div>
    </div>
  </div>
  <div v-else>
    <h1>Cargando api...</h1>
  </div>
</template>
<style lang="css" scoped></style>