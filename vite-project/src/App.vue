<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref } from "vue";
import movie from './components/movie.vue'

const name = ref("Avengers Endgame");
</script>

<template>
  <movie></movie>
</template>

<style scoped>

</style>
