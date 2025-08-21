<script setup>
import { ref } from "vue";

// images ko import karo
import img1 from "@/assets/img1.png";
import img2 from "@/assets/img2.svg";
import img3 from "@/assets/img3.png";
import logo from "@/assets/logo.png";
import profileButton from "@/assets/profile_button.svg";
import bg from "@/assets/launcher-bg.svg";

const firstImage = ref(img3); // default image
const showLoader = ref(false);
const loaderWidth = ref(0);
const loaderText = ref("");

const handlePlay = () => {
  // Step 1: Replace image
  firstImage.value = img1;

  // Step 2: Loader start after delay
  setTimeout(() => {
    showLoader.value = true;
    loaderWidth.value = 0;
    loaderText.value = "Vérification des fichiers ...";

    const animateLoader = async () => {
      await fillTo(50, 40); // 0 → 50
      await pause(800);     // pause 0.8 sec
      await fillTo(70, 40); // 50 → 70
      await pause(1000);    // pause 1 sec
      await fillTo(99, 40); // 70 → 99
      await pause(1200);    // pause 1.2 sec
      await fillTo(100, 60); // 99 → 100
      loaderText.value = "Lancement en cours ..."; 
    };

    animateLoader();
  }, 500);
};
// helper: fill loader step by step
function fillTo(target, speed) {
  return new Promise((resolve) => {
    const interval = setInterval(() => {
      if (loaderWidth.value >= target) {
        clearInterval(interval);
        resolve();
      } else {
        loaderWidth.value++;
        // update text according to stage
        if (loaderWidth.value <= 55) {
          loaderText.value = "Vérification des fichiers ...";
        } else if (loaderWidth.value <= 70) {
          loaderText.value = "Vérification des fichiers ..";
        } else if (loaderWidth.value <= 99) {
          loaderText.value = "Installation de la mise à jour 4.5";
        }
      }
    }, speed);
  });
}

// helper: pause
function pause(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}
</script>

<template>
  <div class="relative w-full min-h-[100vh]">
    <img :src="bg" alt=""
      class="absolute top-0 left-0 w-full h-full object-cover z-0 rounded-br-[30px] rounded-bl-[30px]" />
    <div class="flex items-end min-h-[100vh] rounded-br-[30px] rounded-bl-[30px] overflow-hidden">
      <div
        class="rounded-br-[30px] rounded-bl-[30px] px-5 2xl:!px-[50px] py-[30px] bg-transparent min-h-[50%] gradient_bgc z-40 w-full">
        <!-- main section  -->
        <div
          class="flex justify-center xl:!justify-between flex-col xl:!flex-row items-center gap-[20px] mx-[30px] mb-[50px]">
          <!-- LEFT SIDE -->
          <div class="flex flex-col gap-5 items-center xl:!items-start w-full xl:!w-[40%]">
            <img :src="logo" alt="" class="w-[300px] xl:!w-[50%]" />
            <div class="flex items-center justify-center xl:!justify-start gap-[20px] sm:!flex-row w-full flex-col">
              <button @click="handlePlay"
                class="kanit w-[300px] uppercase h-[75px] 2xl:!h-[136px] 2xl:!w-[500px] btn_yellow_gradient rounded-[20px] 2xl:!rounded-[30px] text-[#151515] text-2xl md:!text-5xl 2xl:text-[80px] font-extrabold flex justify-center items-center">
                <span>Jouer</span>
              </button>
              <img :src="profileButton" alt="" class="w-[90px] xl:!w-[20%]" />
              <i class="fa-solid fa-gear text-white text-[30px]"></i>
            </div>
          </div>

          <!-- RIGHT SIDE -->
          <div
            class="flex items-center justify-center xl:justify-end gap-[50px] w-full xl:!w-[40%] flex-col sm:!flex-row">
            <img :src="firstImage" alt="" class="w-[300px] xl:!w-[70%] rounded-[20px] transition-all duration-500" />
            <img :src="img2" alt="" class="w-[110px] xl:!w-[20%]" />
          </div>
        </div>

        <!-- Loader -->
        <div v-if="showLoader" class="mx-[30px] mb-[20px]">
          <div class="flex justify-between items-center gap-2">
            <div class="relative w-full h-[8px] bg-gray-700 rounded-full overflow-hidden flex items-center">
            <!-- progress bar -->
            <div class="h-full bg-yellow-400 transition-all duration-300" :style="{ width: loaderWidth + '%' }"></div>
            <!-- percentage on right side -->

          </div>
          <span class=" text-white text-sm font-semibold">
            {{ loaderWidth }}%
          </span>
          </div>

          <!-- Loader text under bar -->
          <p class="text-center text-white mt-6 text-base">
            {{ loaderText }}
          </p>
        </div>


        <p
          class="text-base 2xl:!text-xl poppins text-[#FFFFFF] underline opacity-[50%] mx-[30px] absolute bottom-[30px] left-[50px]">
          Contacter le Centre d’aide
        </p>
      </div>
    </div>
  </div>
</template>
