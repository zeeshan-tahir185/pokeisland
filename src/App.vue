<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Header from './components/Header.vue'
</script>

<template>
  <div class="!bg-[#1E1E1E] w-full">
    <div
      class="flex flex-col rounded-[30px] overflow-hidden min-h-[100vh] px-[20px] md:!px-[5%] 2xl:!px-[10%] max-w-[1920px] md:!mx-auto py-[50px] md:!py-[100px]"
    >
      <Header />
      <RouterView />
    </div>
  </div>
</template>
