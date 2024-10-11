<script setup>
import { defineProps } from 'vue';
defineProps({
    anime: {
        type: Object
    }
});
</script>
<template>
    <h1>{{ anime.title }}</h1>
    <img :src="anime.images.jpg.image_url">
</template>
<style scoped></style>