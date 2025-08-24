<script setup>
import { ref } from "vue";

// images
import img1 from "@/assets/img1.png";
import img2 from "@/assets/img2.svg";
import img3 from "@/assets/img3.png";
import logo from "@/assets/logo.png";
import profileButton from "@/assets/profile_button.svg";
import bg from "@/assets/launcher-bg.svg";
import Header from "@/components/Header.vue";

const firstImage = ref(img3);
const showLoader = ref(false);
const loaderWidth = ref(0);
const loaderText = ref("");

// 👇 shrink stage controller
const shrinkStage = ref(0);

const handlePlay = () => {
  firstImage.value = img1;

  setTimeout(() => {
    showLoader.value = true;
    loaderWidth.value = 0;
    loaderText.value = "Vérification des fichiers ...";

    const animateLoader = async () => {
      await fillTo(50, 40);
      await pause(800);
      await fillTo(70, 40);
      await pause(1000);
      await fillTo(99, 40);
      await pause(1200);
      await fillTo(100, 60);
      loaderText.value = "Lancement en cours ...";

      // 👇 after loader complete → start shrink animation
      setTimeout(async () => {
        shrinkStage.value = 1; // 70%
        await pause(600);
        shrinkStage.value = 2; // 40%
        await pause(600);
        shrinkStage.value = 3; // vanish
      }, 800);
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
function openSetting(){
  window.location.href = '/settings'
}
function handleswitchAcc(){
  window.location.href = '/switch-account'
}
// helper: pause
function pause(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}
</script>

<template>
  <div
    class="main-wrapper flex flex-col  overflow-hidden min-h-[100vh] xl:!min-h-[1000px] max-w-[1920px] md:!mx-auto  transition-all duration-700 ease-in-out"
    :class="{
      'shrink-70': shrinkStage === 1,
      'shrink-40': shrinkStage === 2,
      'shrink-vanish': shrinkStage === 3
    }"
  >
    <Header />
    <div class="relative w-full min-h-[100vh] xl:!min-h-[1000px]">
      <img
        :src="bg"
        alt=""
        class="absolute top-0 left-0 w-full h-full object-cover z-0 "
      />
      <div class="flex items-end min-h-[100vh] xl:!min-h-[1000px]  overflow-hidden">
        <div
          class=" px-5 2xl:!px-[50px] py-[30px] bg-transparent min-h-[50%] gradient_bgc z-40 w-full"
        >
          <!-- main section -->
          <div
            class="flex justify-center xl:!justify-between flex-col xl:!flex-row items-center gap-[20px] mx-[30px] mb-[50px]"
          >
            <!-- LEFT -->
            <div class="flex flex-col gap-5 items-center xl:!items-start w-full xl:!w-[40%]">
              <img :src="logo" alt="" class="w-[300px] xl:!w-[50%]" />
              <div
                class="flex items-center justify-center xl:!justify-start gap-[20px] sm:!flex-row w-full flex-col"
              >
                <button
                  @click="handlePlay"
                  class="kanit w-[300px] cursor-pointer uppercase h-[75px] 2xl:!h-[136px] 2xl:!w-[500px] btn_yellow_gradient rounded-[20px] 2xl:!rounded-[30px] text-[#151515] text-2xl md:!text-5xl 2xl:text-[80px] font-extrabold flex justify-center items-center"
                >
                  <span>Jouer</span>
                </button>
                <img :src="profileButton" alt="" class="w-[90px] xl:!w-[20%] cursor-pointer"  @click="handleswitchAcc" />
                <i class="fa-solid fa-gear text-white text-[30px] cursor-pointer" @click="openSetting"></i>
              </div>
            </div>

            <!-- RIGHT -->
            <div
              class="flex items-center justify-center xl:justify-end gap-[50px] w-full xl:!w-[40%] flex-col sm:!flex-row"
            >
              <img
                :src="firstImage"
                alt=""
                class="w-[300px] xl:!w-[70%] rounded-[20px] transition-all duration-500"
              />
              <div class="flex flex-col items-center gap-[50px] bg-[#030305] rounded-[30px] p-[30px]">
                <a href="#"><img src="@/assets/icon1.png" alt="" class="w-[42px] cursor-pointer" /></a>
                <a href="#"><img src="@/assets/icon2.png" alt="" class="w-[36px] cursor-pointer" /></a>
                <a href="#"><img src="@/assets/icon3.png" alt="" class="w-[50px] cursor-pointer" /></a>
              </div>
            </div>
          </div>

          <!-- Loader -->
          <div v-if="showLoader" class="mx-[30px] mb-[20px]">
            <div class="flex justify-between items-center gap-2">
              <div
                class="relative w-full h-[8px] bg-gray-700 rounded-full overflow-hidden flex items-center"
              >
                <div
                  class="h-full bg-yellow-400 transition-all duration-300"
                  :style="{ width: loaderWidth + '%' }"
                ></div>
              </div>
              <span class=" text-white text-sm font-semibold">
                {{ loaderWidth }}%
              </span>
            </div>

            <p class="text-center text-white mt-6 text-base">
              {{ loaderText }}
            </p>
          </div>

          <p
            class="text-base 2xl:!text-xl poppins text-[#FFFFFF] underline opacity-[50%] mx-[30px] absolute bottom-[30px] left-[50px]"
          >
            Contacter le Centre d’aide
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.shrink-70 {
  transform: scale(0.7);
  opacity: 0.9;
}
.shrink-40 {
  transform: scale(0.4);
  opacity: 0.6;
}
.shrink-vanish {
  transform: scale(0.2);
  opacity: 0;
  pointer-events: none;
}
</style>
