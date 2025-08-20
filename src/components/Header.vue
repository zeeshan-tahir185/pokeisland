<script setup>
import { MinusIcon, XMarkIcon } from '@heroicons/vue/24/outline' // Use outline or solid as needed
</script>

<template>
  <div
    class="h-[64px] w-full bg-[#2B2B2B] rounded-tr-[30px] rounded-tl-[30px] flex justify-start md:justify-center px-[30px] items-center relative"
  >
    <h2 class="text-base md:text-xl font-semibold text-white kanit">POKEISLAND LAUNCHER</h2>
    <div
      class="flex justify-center items-center absolute right-[30px] md:right-[50px] gap-[20px] md:gap-[50px]"
    >
      <MinusIcon class="h-6 w-6 text-[#878787]" />
      <XMarkIcon class="h-6 w-6 text-[#878787]" />
    </div>
  </div>
</template>
