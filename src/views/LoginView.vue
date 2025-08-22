<script setup>
import { ref } from 'vue'
import Header from '@/components/Header.vue'
</script>

<template>
  <div
    class="main-wrapper flex flex-col rounded-[30px] overflow-hidden min-h-[100vh] xl:!min-h-[1000px] px-[20px] md:!px-[5%] max-w-[1920px] md:!mx-auto py-[50px] md:!py-[100px] transition-all duration-700 ease-in-out"
  >
    <Header />
    <div class="relative w-full min-h-[100vh] xl:!min-h-[1014px]">
      <img
        src="@/assets/login/login1.png"
        alt=""
        class="absolute top-0 left-0 w-full h-full object-cover z-0 rounded-br-[30px] rounded-bl-[30px]"
      />
    </div>
    <div>
        
    </div>
  </div>
</template>
