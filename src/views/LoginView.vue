<script setup>
import { ref } from 'vue'
import Header from '@/components/Header.vue'

const closeModal = () => {
  window.location.href = '/' // agar vue-router use kar rahe ho to: router.push("/")
}
function changeModal(){
  window.location.href = '/login/steps'
}
</script>

<template>
  <div
    class="main-wrapper flex flex-col rounded-[30px] overflow-hidden min-h-[100vh] xl:!min-h-[1000px] px-[20px] md:!px-[5%] max-w-[1920px] md:!mx-auto py-[50px] md:!py-[100px] transition-all duration-700 ease-in-out"
  >
    <Header />
    <div class="relative w-full min-h-[100vh] xl:!min-h-[1014px] flex justify-center items-center">
      <img
        src="@/assets/login/login1.png"
        alt=""
        class="absolute top-0 left-0 w-full h-full object-cover z-0 rounded-br-[30px] rounded-bl-[30px]"
      />
      <div
        class="relative w-full m-[20px] md:!w-[666px] min-h-[709px] rounded-[30px] border-[3px] border-[#434343] bg-[#2B2B2B] !z-50 flex flex-col gap-[20px] p-[30px] md:!p-[50px]"
      >
        <button
          class="absolute top-5 right-5 text-gray-400 hover:text-white text-xl cursor-pointer"
          @click="closeModal"
        >
          ✕
        </button>
        <img src="@/assets/login/img1.png" alt="" class="w-[250px] mx-auto mb-[30px]" />
        <p class="poppins text-white text-[19px]">
          De quel compte souhaitez-vous vous déconnecter ?
        </p>
        <div
          class="poppins hover:!bg-[#222222] flex items-start md:!items-center gap-3 !p-3 bg-[#2c2c2c] rounded-lg cursor-pointer flex-col lg:!flex-row"
        >
          <img src="@/assets/setting/profile.svg" alt="profile" class="w-[135px] rounded-md" />
          <div class="flex flex-col justify-start text-start gap-[10px]">
            <p class="text-white text-[32px]">TheDiamondMinecart</p>
            <p class="text-base text-[#A7A7A7]">septminecraft@gmail.com</p>
            <p class="text-[#6BE500] text-base">
              Connecté <i class="fa-regular fa-circle-check"></i>
            </p>
          </div>
        </div>
        <div
          class="poppins hover:!bg-[#222222] flex items-start md:!items-center gap-3 !p-3 bg-[#2c2c2c] rounded-lg cursor-pointer flex-col lg:!flex-row"
        >
          <img src="@/assets/login/img2.png" alt="profile" class="w-[135px] rounded-md" />
          <div class="flex flex-col justify-start text-start gap-[10px]">
            <p class="text-white text-[32px]">Treste99</p>
            <p class="text-base text-[#A7A7A7]">yoptoutlemondecesttreste99@gmail.com</p>
            <p class="text-red-700 text-base">Deconnecté</p>
          </div>
        </div>
        <div class="border-b-[3px] border-[#434343] w-full mt-[20px]"></div>
        <button
          class="cursor-pointer w-full md:!w-[547px] mt-[20px] h-[67px] rounded-[15px] bg-[#2B8746] flex justify-center items-center font-medium text-base text-white"
        @click="changeModal"
          >
          Ajouter un compte
        </button>
      </div>
    </div>
  </div>
</template>
