<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Header from './components/Header.vue'
</script>

<template>
  <div class="flex flex-col rounded-[300px] max-w-[1920px] mx-auto">
    <Header />
    <RouterView />
  </div>
</template>
