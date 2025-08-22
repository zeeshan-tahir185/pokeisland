<script setup>
import { ref } from "vue";

// launcher files state
const launcherFiles = ref([])
// client files state
const clientFiles = ref([])

// Handle file upload
const handleFileUpload = (event, type) => {
  const files = event.target.files
  if (!files.length) return

  const targetArray = type === "launcher" ? launcherFiles : clientFiles

  for (let file of files) {
    targetArray.value.push({
      name: file.name,
      version: "v1.0.0.2", // dummy version (aap apne backend/API se real version le sakte ho)
      enabled: true,
    })
  }
  event.target.value = "" // reset input
}

// Delete file
const deleteFile = (type, index) => {
  const targetArray = type === "launcher" ? launcherFiles : clientFiles
  targetArray.value.splice(index, 1)
}

// Toggle enable/disable
const toggleFile = (type, index) => {
  const targetArray = type === "launcher" ? launcherFiles : clientFiles
  targetArray.value[index].enabled = !targetArray.value[index].enabled
}
// RAM Slider State
const ram = ref(4);
</script>

<template>
  <div class="text-white w-full h-full px-[10px] xl:!px-[30px] !py-[50px]">
    <h2 class="text-2xl md:!text-3xl font-bold mb-[20px] md:!mb-[50px] text-center md:!text-start">
      Paramètres de Java
    </h2>

    <!-- Scrollable content wrapper -->
    <div class="flex flex-col gap-6 max-h-[700px] overflow-y-auto !pr-2 xl:!pr-[30px] custom-scroll">
      <!-- First Section: Memory Settings -->
      <div class="flex flex-col gap-[20px]">
        <div class="flex justify-between items-center gap-[20px] flex-col lg:!flex-row">
          <div>
            <p class="text-base md:!text-lg xl:!text-[26px] font-bold text-white">
              Mémoire
            </p>
            <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">
              Configurer votre RAM
            </p>
          </div>
          <div class="flex items-center gap-[10px] flex-col sm:!flex-row">
            <div
              class="flex justify-center items-center mt-2 flex-col border-2 border-[#434343] h-[92px] px-[30px] py-[10px] rounded-[10px]">
              <span class="text-white poppins font-bold text-xl lg:!text-[26px]">RAM</span>
              <span
                class="text-white font-bold h-[32px] bg-[#434343] rounded-[30px] w-[92px] flex justify-center items-center">{{
                  ram }}G</span>
            </div>
            <div
              class="flex justify-center items-center mt-2 flex-col border-2 border-[#434343] h-[92px] px-[30px] py-[10px] rounded-[10px]">
              <span class="text-white poppins font-bold text-xl lg:!text-[26px]">Total</span>
              <span class="text-[#9D9D9D] text-lg lg:!text-[22px]">9.7G</span>
            </div>
            <div
              class="flex justify-center items-center mt-2 flex-col border-2 border-[#434343] h-[92px] px-[30px] py-[10px] rounded-[10px]">
              <span class="text-white poppins font-bold text-xl lg:!text-[26px]">Disponible</span>
              <span class="text-[#9D9D9D] text-lg lg:!text-[22px]">14.9G</span>
            </div>

          </div>
        </div>

        <!-- Memory Slider -->
        <div class="relative w-full">
          <!-- Slider -->
          <input type="range" min="2" max="16" v-model.number="ram" step="1"
            class="w-full h-2 bg-[#434343] rounded-full appearance-none cursor-pointer" :style="{
              background: `linear-gradient(to right, #ffffff ${(ram - 2) * (100 / 14)}%, #434343 ${(ram - 2) * (100 / 14)}%)`
            }" />

          <!-- Ticks (Slider points) -->
          <div class="absolute w-full flex justify-between text-sm text-white mt-2">
            <span>2G</span>
            <span>3G</span>
            <span>4G</span>
            <span>5G</span>
            <span>6G</span>
            <span>7G</span>
            <span>8G</span>
            <span>9G</span>
            <span>10G</span>
            <span>11G</span>
            <span>12G</span>
            <span>13G</span>
            <span>14G</span>
            <span>15G</span>
            <span>16G</span>
          </div>
        </div>


      </div>

      <!-- Divider Line -->
      <div class="border-b-[3px] border-[#434343] w-full mt-[20px]"></div>
    </div>
    <div class="flex flex-col mt-[20px]">
      <p class="text-base md:!text-lg xl:!text-[26px] text-white">Installation de Java</p>
      <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">
        Votre version actuelle : Java 21.0.7 (Eclipse Adoptium)
      </p>
      <div
        class="mt-[20px] flex items-center gap-2 border border-[#434343] rounded-lg overflow-hidden w-full lg:!w-[801px] h-[52px] !px-3">
        <input type="text" readonly value="C:\Users\AppData\Roaming\.pokeisland\runtime\x64\jdk-21.0.7+6\bin\javaw.exe"
          class="flex-1 !bg-transparent px-4 py-2 white outline-none cursor-default text-xs md:!text-base" />
        <label
          class="bg-[#434343] transition w-[100px] md:!w-[195px] h-[32px] cursor-pointer text-[10px] md:text-base flex justify-center items-center rounded-[10px]">
          Choisir un fichier
          <input type="file" class="hidden" multiple @change="(e) => handleFileUpload(e, 'launcher')" />
        </label>
      </div>

      <!-- Uploaded launcher files -->
      <div v-if="launcherFiles.length" class="mt-4 flex flex-col gap-3">
        <div v-for="(file, index) in launcherFiles" :key="index"
          class="flex justify-between items-center bg-[#2D2D2D] mt-[20px] rounded-lg !px-4 w-full h-[87px] ">
          <div>
            <p class="font-medium">{{ file.name }}</p>
            <p class="text-xs text-gray-400">{{ file.version }}</p>
          </div>
          <div class="flex items-center gap-3">
            <!-- delete -->
            <button @click="deleteFile('launcher', index)"
              class="text-gray-400 text-base md:!text-[24px] hover:text-red-500">
              <i class="fa-solid fa-trash"></i>
            </button>
            <!-- toggle -->
            <label class="relative inline-flex items-center cursor-pointer">
              <input type="checkbox" class="sr-only peer" :checked="file.enabled"
                @change="toggleFile('launcher', index)" />
              <div
                class="w-11 xl:!w-[80px] h-6 xl:!h-[50px] bg-[#434343] rounded-full peer peer-checked:!bg-white transition-all">
              </div>
              <div
                class="absolute left-1 xl:!left-[8px] top-1 xl:!top-[9px] bg-[#2B2B2B] w-4 xl:!w-[30px] h-4 xl:!h-[30px] rounded-full peer-checked:translate-x-5 xl:peer-checked:!translate-x-9 transition-all">
              </div>
            </label>
          </div>
        </div>
      </div>
    </div>
    <div class="flex flex-col mt-[20px]">
      <p class="text-base md:!text-lg xl:!text-[26px] text-white">Options JVM Supplémentaires</p>
      <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">
        -Xms et -Xmx ne doivent pas être inclus.
      </p>
      <div
        class="mt-[20px] flex items-center gap-2 border border-[#434343] rounded-lg overflow-hidden w-full xl:!w-[871px] h-[52px] !px-3">
        <input type="text" readonly
          value="-XX:+UnlockExperimentalVMOptions -XX:+UseG1GC -XX:G1NewSizePercent=20 -XX:G1ReservePercent=20 -XX:MaxGCPauseMillis=50 -XX:G1HeapRegionSize=32M"
          class="flex-1 !bg-transparent px-4 py-2 white outline-none cursor-default text-xs md:!text-base" />
      </div>
      <p class="poppins text-sm text-[#FFE400] underline mt-[10px]">Options disponibles pour Java 21 (HotSpot VM)</p>
    </div>
  </div>
</template>

<style scoped>
.custom-scroll::-webkit-scrollbar {
  width: 10px;
}

.custom-scroll::-webkit-scrollbar-track {
  background: #2c2c2c;
  border-radius: 10px;
}

.custom-scroll::-webkit-scrollbar-thumb {
  background: #ffffff;
  border-radius: 10px;
}

.custom-scroll::-webkit-scrollbar-thumb:hover {
  background: #d9d9d9;
}

/* Custom Slider Thumb */
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 16px;
  height: 16px;
  background: #ffffff;
  border-radius: 50%;
  cursor: pointer;
  border: 2px solid #000000;
  margin-top: -7px;
  /* Center the thumb on the 2px track */
}

input[type="range"]::-moz-range-thumb {
  width: 16px;
  height: 16px;
  background: #ffffff;
  border-radius: 50%;
  cursor: pointer;
  border: 2px solid #000000;
}

/* Custom Slider Track */
input[type="range"]::-webkit-slider-runnable-track {
  -webkit-appearance: none;
  height: 2px;
  border-radius: 2px;
}

input[type="range"]::-moz-range-track {
  height: 2px;
  border-radius: 2px;
}

/* Ensure tick marks align with slider steps */
input[type="range"] {
  padding: 0;
  margin: 0;
}

@media (max-width: 1024px) {
  .text-base {
    font-size: 14px;
  }

  .text-sm {
    font-size: 12px;
  }

  .text-white {
    font-size: 12px;
  }

  .absolute span {
    margin-left: 4px;
    margin-right: 4px;
  }
}

@media (max-width: 768px) {
  .text-base {
    font-size: 12px;
  }

  .text-sm {
    font-size: 10px;
  }

  .text-white {
    font-size: 10px;
  }

  .absolute span {
    margin-left: 2px;
    margin-right: 2px;
  }
}
</style>
