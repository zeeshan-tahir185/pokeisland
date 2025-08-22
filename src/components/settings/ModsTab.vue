<script setup>
import { ref } from "vue"

// launcher files state
const launcherFiles = ref([])
// shaders files state
const shadersFiles = ref([])

// Handle file upload
const handleFileUpload = (event, type) => {
    const files = event.target.files
    if (!files.length) return

    const targetArray = type === "launcher" ? launcherFiles : shadersFiles

    for (let file of files) {
        targetArray.value.push({
            name: file.name,
            version: "v1.0.0.2", // dummy version (you can replace with a real version from your backend/API)
            enabled: true,
        })
    }
    event.target.value = "" // reset input
}

// Delete file
const deleteFile = (type, index) => {
    const targetArray = type === "launcher" ? launcherFiles : shadersFiles
    targetArray.value.splice(index, 1)
}

// Toggle enable/disable
const toggleFile = (type, index) => {
    const targetArray = type === "launcher" ? launcherFiles : shadersFiles
    targetArray.value[index].enabled = !targetArray.value[index].enabled
}
</script>

<template>
    <div class="text-white w-full h-full px-[10px] xl:!px-[30px] !py-[50px]">
        <h2 class="text-2xl md:text-3xl font-bold mb-[20px] md:!mb-[50px] text-center md:!text-start">Paramètres des
            Mods</h2>

        <!-- Scrollable content wrapper -->
        <div class="flex flex-col gap-6 max-h-[700px] overflow-y-auto !pr-2 xl:!pr-[30px] custom-scroll">

            <!-- Required Mods -->
            <div class="flex flex-col gap-[20px]">
                <div class="flex justify-between items-start flex-col gap-[20px]">
                    <p class="text-base md:!text-lg xl:!text-[26px] font-bold text-white">Mods du Launcher</p>
                    <div class="relative w-full">
                        <select
                            class="appearance-none outline-none bg-[#2B2B2B] text-white rounded-[10px] h-[70px] md:!h-[100px] border-2 border-[#434343] w-full poppins font-bold text-xl md:text-[26px] px-[10px]">
                            <option>Mads raquis</option>
                            <option>Mads raquis</option>
                        </select>
                        <img src="@/assets/setting/arrow.png" alt="" class="absolute top-[30px] md:!top-[45px] right-3">
                    </div>
                </div>
                <div class="border-b-[3px] border-[#434343] w-full"></div>
            </div>

            <!-- Mods additionnels Section -->
            <div class="flex flex-col">
                <p class="text-base md:!text-lg xl:!text-[26px] font-bold text-white">Mods additionnels</p>
                <div
                    class="mt-[20px] flex items-center gap-2 border-dashed border-[#D7D7D7] rounded-lg overflow-hidden w-full h-[70px] md:!h-[100px]">
                    <input type="text" readonly placeholder="Apparaître un mod"
                        class="flex-1 hidden !bg-transparent  white outline-none cursor-default text-xs md:!text-base" />
                    <label
                        class="bg-[#434343] border border-dashed border-[#D7D7D7] transition w-[100%] h-full cursor-pointer text-base md:!text-[22px] flex justify-center items-center rounded-[10px]">
                        Ajouter un mod +
                        <input type="file" class="hidden" multiple @change="(e) => handleFileUpload(e, 'launcher')" />
                    </label>
                </div>

                <!-- Uploaded launcher files -->
                <div v-if="launcherFiles.length" class="mt-4 flex flex-col gap-3">
                    <div v-for="(file, index) in launcherFiles" :key="index"
                        class="flex justify-between items-center bg-[#2D2D2D] mt-[20px] rounded-lg !px-4 w-full h-[87px]">
                        <div>
                            <p class="font-medium">{{ file.name }}</p>
                            <p class="text-xs text-gray-400">{{ file.version }}</p>
                        </div>
                        <div class="flex items-center gap-3">
                            <button @click="deleteFile('launcher', index)"
                                class="text-gray-400 text-base md:!text-[24px] hover:text-red-500">
                                <i class="fa-solid fa-trash"></i>
                            </button>
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
                <div class="border-b-[3px] border-[#434343] mt-[20px] w-full"></div>
            </div>

            <!-- Shaders Section -->
            <div class="flex flex-col">
                <p class="text-base md:!text-lg xl:!text-[26px] font-bold text-white mb-[20px]">Shaders</p>
                <div class="w-full flex justify-center items-center gap-[20px] flex-col md:!flex-row">
                    <div class="relative w-full md:!w-[49%]">
                        <select
                            class="appearance-none outline-none bg-[#2B2B2B] text-white rounded-[10px] h-[70px] md:!h-[100px] border-2 border-[#434343] w-full poppins font-bold text-xl md:text-[26px] px-[10px]">
                            <option>OFF</option>
                            <option>ON</option>
                        </select>
                        <img src="@/assets/setting/arrow.png" alt="" class="absolute top-[30px] md:!top-[45px] right-3">
                    </div>
                    <div
                        class="flex items-center gap-2 border-dashed border-[#D7D7D7] rounded-lg overflow-hidden w-full md:!w-[49%] h-[70px] md:!h-[100px]">
                        <input type="text" readonly placeholder="Apparaître un mod"
                            class="flex-1 hidden !bg-transparent  white outline-none cursor-default text-xs md:!text-base" />
                        <label
                            class="bg-[#434343] border border-dashed border-[#D7D7D7] transition w-[100%] h-full cursor-pointer text-base md:!text-[22px] flex justify-center items-center rounded-[10px]">
                            Ajouter un mod +
                            <input type="file" class="hidden" multiple @change="(e) => handleFileUpload(e, 'client')" />
                        </label>
                    </div>
                </div>

                <!-- Uploaded shaders files -->
                <div v-if="shadersFiles.length" class="mt-4 flex flex-col gap-3">
                    <div v-for="(file, index) in shadersFiles" :key="index"
                        class="flex justify-between items-center bg-[#2D2D2D] mt-[20px] rounded-lg !px-4 w-full h-[87px]">
                        <div>
                            <p class="font-medium">{{ file.name }}</p>
                            <p class="text-xs text-gray-400">{{ file.version }}</p>
                        </div>
                        <div class="flex items-center gap-3">
                            <button @click="deleteFile('client', index)"
                                class="text-gray-400 text-base md:!text-[24px] hover:text-red-500">
                                <i class="fa-solid fa-trash"></i>
                            </button>
                            <label class="relative inline-flex items-center cursor-pointer">
                                <input type="checkbox" class="sr-only peer" :checked="file.enabled"
                                    @change="toggleFile('client', index)" />
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
                <div class="border-b-[3px] border-[#434343] mt-[20px] w-full"></div>
            </div>
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
</style>
