<script setup>
/* apni background image ko /src/assets/launcher-bg.jpg me rakho */
</script>

<template>
  <div class="relative w-full min-h-[100vh]">
    <img
      src="@/assets/launcher-bg.svg"
      alt=""
      class="absolute top-0 left-0 w-full h-full object-cover z-0 rounded-br-[30px] rounded-bl-[30px]"
    />
    <div class="flex items-end min-h-[100vh] rounded-br-[30px] rounded-bl-[30px] overflow-hidden">
      <div
        class="flex rounded-br-[30px] rounded-bl-[30px] justify-center xl:!justify-between flex-col xl:!flex-row items-center gap-[20px] px-5 2xl:!px-[50px] py-[30px] bg-transparent min-h-[50%] gradient_bgc z-40 w-full"
      >
        <div class="flex flex-col gap-5 items-center xl:!items-start w-full xl:!w-[40%]">
          <img src="@/assets/logo.png" alt="" class="w-[300px] xl:!w-[50%]" />
          <div
            class="flex items-center justify-center xl:!justify-start gap-[20px] sm:!flex-row w-full flex-col"
          >
            <button
              class="kanit w-[300px] uppercase h-[75px] 2xl:!h-[136px] 2xl:!w-[500px] btn_yellow_gradient rounded-[20px] 2xl:!rounded-[30px] text-[#151515] text-2xl md:!text-5xl 2xl:text-[80px] font-extrabold flex justify-center items-center"
            >
              <span>Jouer</span>
            </button>
            <img src="@/assets/profile_button.svg" alt="" class="w-[90px] xl:!w-[20%]" />
            <i class="fa-solid fa-gear text-white text-[30px]"></i>
          </div>
          <p class="text-base 2xl:!text-xl poppins text-[#FFFFFF] underline opacity-[50%]">
            Contacter le Centre d’aide
          </p>
        </div>
        <div
          class="flex items-center justify-center xl:justify-end gap-[50px] w-full xl:!w-[40%] flex-col sm:!flex-row"
        >
          <img src="@/assets/img3.png" alt="" class="w-[300px] xl:!w-[70%] rounded-[20px]" />
          <img src="@/assets/img2.svg" alt="" class="w-[110px] xl:!w-[20%]" />
        </div>
      </div>
    </div>
  </div>
</template>
