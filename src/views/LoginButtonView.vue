<script setup>
import { ref } from 'vue'

import logo from '@/assets/logo2.png'
import bg from '@/assets/launcher-bg.svg'
import Header from '@/components/Header.vue'


// 👇 shrink stage controller
const shrinkStage = ref(0)

const handlePlay = () => {
  const alreadyClicked = localStorage.getItem('isFirstLoginClicked')

  if (alreadyClicked) {
    // agar pehle click ho chuka hai
    window.location.href = '/switch-account'
  } else {
    // pehli dafa click
    localStorage.setItem('isFirstLoginClicked', 'true')
    window.location.href = '/login/steps'
  }
}

</script>

<template>
  <div
    class="main-wrapper flex flex-col rounded-[30px] overflow-hidden min-h-[100vh] xl:!min-h-[1000px] px-[20px] md:!px-[5%] max-w-[1920px] md:!mx-auto py-[50px] md:!py-[100px] transition-all duration-700 ease-in-out"
    :class="{
      'shrink-70': shrinkStage === 1,
      'shrink-40': shrinkStage === 2,
      'shrink-vanish': shrinkStage === 3,
    }"
  >
    <Header />
    <div class="relative w-full min-h-[100vh] xl:!min-h-[1000px]">
      <img
        :src="bg"
        alt=""
        class="absolute top-0 left-0 w-full h-full object-cover z-0 rounded-br-[30px] rounded-bl-[30px]"
      />
      <div
        class="flex items-end min-h-[100vh] xl:!min-h-[1000px] rounded-br-[30px] rounded-bl-[30px] overflow-hidden"
      >
        <div
          class="rounded-br-[30px] rounded-bl-[30px] px-5 2xl:!px-[50px] py-[30px] bg-transparent min-h-[50%] gradient_bgc z-40 w-full"
        >
          <!-- main section -->
          <div
            class="flex justify-center xl:!justify-between flex-col xl:!flex-row items-center gap-[20px] mx-[30px] mb-[50px]"
          >
            <!-- LEFT -->
            <div class="flex flex-col gap-5 items-center  w-full ">
              <img :src="logo" alt="" class="w-[300px] xl:!w-[50%] mb-[-80px]" />
              <button
                @click="handlePlay"
                class="kanit w-[300px] cursor-pointer uppercase h-[75px] 2xl:!h-[136px] 2xl:!w-[500px] btn_yellow_gradient rounded-[20px] 2xl:!rounded-[30px] text-[#151515] text-2xl md:!text-5xl 2xl:text-[80px] font-extrabold flex justify-center items-center"
              >
                <span>Connexion</span>
              </button>
              <p
                class="text-base 2xl:!text-xl poppins text-[#FFFFFF] underline opacity-[50%] mx-[30px] "
              >
                Contacter le Centre d’aide
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
