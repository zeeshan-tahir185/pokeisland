<script setup>
import { ref } from 'vue'
import Header from '@/components/Header.vue'

const step = ref(1) // abhi kis step pe ho

const closeModal = () => {
  window.location.href = '/' // agar vue-router use kar rahe ho to: router.push("/")
}

const nextStep = () => {
  if (step.value < 4) {
    step.value++
  }
}

const prevStep = () => {
  if (step.value > 1) {
    step.value--
  }
}
</script>

<template>
  <div
    class="main-wrapper flex flex-col rounded-[30px] overflow-hidden min-h-[100vh] xl:!min-h-[1000px] px-[20px] md:!px-[5%] max-w-[1920px] md:!mx-auto py-[50px] md:!py-[100px] transition-all duration-700 ease-in-out"
  >
    <Header />
    <div class="relative w-full min-h-[100vh] xl:!min-h-[1014px] flex justify-center items-center">
      <img
        src="@/assets/login/login2.png"
        alt=""
        class="absolute top-0 left-0 w-full h-full object-cover z-0 rounded-br-[30px] rounded-bl-[30px]"
      />
      <div
        class="relative w-full m-[20px] md:!w-[666px] min-h-[709px] rounded-[30px] border-[3px] border-[#434343] bg-[#2B2B2B] !z-50 flex flex-col gap-[20px] p-[30px] md:!p-[50px]"
      >
        <!-- Close button -->
        <button
          class="absolute top-5 right-5 text-gray-400 hover:text-white text-xl cursor-pointer"
          @click="closeModal"
        >
          ✕
        </button>

        <!-- Back arrow (show only if step > 1) -->
        <button
          v-if="step > 1"
          class="absolute top-5 left-5 text-gray-400 hover:text-white text-3xl cursor-pointer"
          @click="prevStep"
        >
          ←
        </button>

        <!-- Step 1 -->
        <div v-if="step === 1" class="flex flex-col gap-6">
          <img src="@/assets/login/img1.png" alt="" class="w-[250px] mx-auto mb-[100px]" />
          <div class="flex flex-col justify-center items-center gap-2 mb-[30px]">
            <h2 class="text-base md:!text-lg xl:!text-[26px] text-white font-semibold">
              Se connecter
            </h2>
            <p class="poppins text-white text-[19px]">Utilisez votre compte Microsoft.</p>
          </div>

          <div class="flex flex-col gap-4">
            <input
              type="text"
              placeholder="Adresse e-mail ou numéro de téléphone"
              class="w-full md:!w-[547px] h-[50px] rounded-[10px] bg-transparent text-white !px-4 focus:outline-none border border-[#434343]"
            />
            <p class="text-[#28a44d] text-base font-semibold">
              Vous avez oublié votre nom d'utilisateur ?
            </p>
            <button
              class="cursor-pointer w-full md:!w-[547px] h-[67px] my-[30px] rounded-[15px] bg-[#2B8746] flex justify-center items-center font-medium text-base text-white"
              @click="nextStep"
            >
              Suivant
            </button>
            <p class="text-[#28a44d] text-base text-center font-semibold">
              <span class="text-white">Vous débutez avec Microsoft ?</span> Créez un compte
            </p>
          </div>
        </div>

        <!-- Step 2 -->
        <div v-if="step === 2" class="flex flex-col gap-6">
          <img src="@/assets/login/img1.png" alt="" class="w-[250px] mx-auto mb-[100px]" />
          <p
            class="text-white text-center rounded-full bg-transparent h-[48px] mx-auto w-[250px] text-lg flex justify-center items-center border-2 border-[#434343]"
          >
            septminecraft@gmail.com
          </p>
          <h2 class="text-white text-[35px] font-bold text-center">
            Obtenez un code pour vous connecter
          </h2>
          <p class="text-gray-300 text-center text-xl">
            Nous vous enverrons un code à
            <span class="font-semibold">septminecraft@gmail.com</span> pour vous connecter.
          </p>
          <button
            class="cursor-pointer w-full h-[60px] rounded-[15px] bg-[#2B8746] text-white text-center"
            @click="nextStep"
          >
            Envoyer le code
          </button>
          <p class="text-[#2B8746] text-center text-lg">Autres méthodes pour se connecter</p>
        </div>

        <div v-if="step === 3" class="flex flex-col gap-6">
          <img src="@/assets/login/img1.png" alt="" class="w-[250px] mx-auto mb-[100px]" />
          <p
            class="text-white text-center rounded-full bg-transparent h-[48px] mx-auto w-[250px] text-lg flex justify-center items-center border-2 border-[#434343]"
          >
            septminecraft@gmail.com
          </p>
          <h2 class="text-white text-[35px] font-bold text-center">Entrez votre code</h2>
          <p class="text-gray-300 text-center text-xl">
            Entrez le code que nous avons envoyé à septminecraft@gmail.com.
          </p>
          <div class="flex justify-center gap-2 my-[20px]">
            <input type="text" class="w-12 h-12 text-center text-white  border border-[#434343] rounded-[10px]" maxlength="1" />
            <input type="text" class="w-12 h-12 text-center text-white  border border-[#434343] rounded-[10px]" maxlength="1" />
            <input type="text" class="w-12 h-12 text-center text-white  border border-[#434343] rounded-[10px]" maxlength="1" />
            <input type="text" class="w-12 h-12 text-center text-white  border border-[#434343] rounded-[10px]" maxlength="1" />
            <input type="text" class="w-12 h-12 text-center text-white  border border-[#434343] rounded-[10px]" maxlength="1" />
            <input type="text" class="w-12 h-12 text-center text-white  border border-[#434343] rounded-[10px]" maxlength="1" />
          </div>
          <p class="text-[#2B8746] text-center text-xl cursor-pointer" @click="nextStep" >Vous n'avez pas obtenu de code ?</p>
        </div>
        <!-- Step 3 -->
        <div v-if="step === 4" class="flex flex-col gap-6">
          <img src="@/assets/login/img1.png" alt="" class="w-[250px] mx-auto mb-[100px]" />
          <p
            class="text-white text-center rounded-full bg-transparent h-[48px] mx-auto w-[250px] text-lg flex justify-center items-center border-2 border-[#434343]"
          >
            septminecraft@gmail.com
          </p>
          <h2 class="text-white text-[35px] font-bold text-center">Rester connecté ?</h2>
          <img src="@/assets/login/login3.png" alt="" class="w-[300px] mx-auto">
          <p class="text-gray-300 text-center text-xl">
            Vous n'avez pas à vous connecter à chaque fois. <span class="text-[#2B8746]">En savoir plus</span>
          </p>
          <button
            class="cursor-pointer w-full h-[60px] mt-auto rounded-[15px] bg-[#2B8746] text-white"
            @click="closeModal"
          >
            Oui
          </button>
          <button
            class="cursor-pointer w-full h-[60px] mt-auto rounded-[15px] bg-transparent text-white border-2 border-[#434343] "
            @click="closeModal"
          >
            Non
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
