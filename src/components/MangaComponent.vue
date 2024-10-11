<script setup>
import { defineProps } from 'vue';
defineProps({
    manga: {
        type: Object
    }
});
</script>

<template>
    <div v-if="manga">
        <h1>{{ manga.title }}</h1>
        <img :src="manga.images.jpg.image_url" :alt="manga.title" />
        <p>Status: {{ manga.status }}</p>
        <h3>Títulos alternativos:</h3>
        <ul>
            <!-- Iterar sobre los títulos alternativos -->
            <li v-for="(title, index) in manga.titles" :key="index">
                {{ title.title }} ({{ title.type }})
            </li>
        </ul>
    </div>
    <div v-else>
        <h1>Cargando api...</h1>
    </div>
</template>

<style scoped></style>