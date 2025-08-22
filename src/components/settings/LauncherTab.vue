<script setup>
import { ref } from "vue"

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
</script>
<template>
    <div class="text-white w-full h-full xl: px-[10px] md:!px-[30px] !py-[50px] ">
        <!-- Heading -->
        <h2 class="text-2xl md:text-3xl font-bold mb-[20px] md:!mb-[50px] text-center md:!text-start">Paramètres du Launcher</h2>

        <!-- Scrollable content wrapper -->
        <div class="flex flex-col gap-6  max-h-[700px]  overflow-y-auto !pr-2 xl:!pr-[30px] custom-scroll ">
            <!-- Resolution -->
            <div class="flex flex-col gap-[20px]">
                <div class="flex justify-between items-center flex-col md:!flex-row gap-[20px]">
                    <div class="flex flex-col">
                        <p class="text-base md:!text-lg xl:!text-[26px] text-white">Résolution de l’écran</p>
                        <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">Configurer la fenêtre du jeu.</p>
                    </div>
                    <div class="flex items-center gap-4">
                        <span
                            class="bg-[#434343] border border-[#434343] px-4 py-2 rounded-[30px] w-[118px] h-[50px] text-white flex justify-center items-center text-base xl:text-[26px] poppins">
                            1854
                        </span>
                        <span class="text-xl">×</span>
                        <span
                            class="bg-[#434343] border border-[#434343] px-4 py-2 rounded-[30px] w-[118px] h-[50px] text-white flex justify-center items-center text-base xl:text-[26px] poppins">
                            854
                        </span>
                    </div>
                </div>
                <div class="border-b-[3px] border-[#434343] w-full"></div>
            </div>

            <!-- Plein écran -->
            <div class="flex justify-between items-start md:!items-center pb-4">
                <div>
                    <p class="text-base md:!text-lg xl:!text-[26px] text-white">Plein écran</p>
                    <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">Activer le mode plein écran au lancement du jeu.
                    </p>
                </div>
                <label class="relative inline-flex items-center cursor-pointer">
                    <input type="checkbox" class="sr-only peer" />
                    <div
                        class="w-11 xl:!w-[80px] h-6 xl:!h-[50px] bg-[#434343] rounded-full peer peer-checked:!bg-white transition-all">
                    </div>
                    <div
                        class="absolute left-1 xl:!left-[8px] top-1 xl:!top-[9px] bg-[#2B2B2B] w-4 xl:!w-[30px] h-4 xl:!h-[30px] rounded-full peer-checked:translate-x-5 xl:peer-checked:!translate-x-9 transition-all">
                    </div>
                </label>
            </div>

            <!-- Connexion automatique -->
            <div class="flex justify-between items-start md:!items-center pb-4">
                <div>
                    <p class="text-base md:!text-lg xl:!text-[26px] text-white">Connexion automatique</p>
                    <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">Se connecter automatiquement au serveur au
                        lancement.</p>
                </div>
                <label class="relative inline-flex items-center cursor-pointer">
                    <input type="checkbox" class="sr-only peer" />
                    <div
                        class="w-11 xl:!w-[80px] h-6 xl:!h-[50px] bg-[#434343] rounded-full peer peer-checked:!bg-white transition-all">
                    </div>
                    <div
                        class="absolute left-1 xl:!left-[8px] top-1 xl:!top-[9px] bg-[#2B2B2B] w-4 xl:!w-[30px] h-4 xl:!h-[30px] rounded-full peer-checked:translate-x-5 xl:peer-checked:!translate-x-9 transition-all">
                    </div>
                </label>
            </div>

            <!-- Mode réduit -->
            <div class="flex justify-between items-start md:!items-center pb-4">
                <div>
                    <p class="text-base md:!text-lg xl:!text-[26px] text-white">Démarrer le launcher en mode réduit</p>
                    <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">Ouvrir le launcher réduit dans la barre des
                        tâches.</p>
                </div>
                <label class="relative inline-flex items-center cursor-pointer">
                    <input type="checkbox" checked class="sr-only peer" />
                    <div
                        class="w-11 xl:!w-[80px] h-6 xl:!h-[50px] bg-[#434343] rounded-full peer peer-checked:!bg-white transition-all">
                    </div>
                    <div
                        class="absolute left-1 xl:!left-[8px] top-1 xl:!top-[9px] bg-[#2B2B2B] w-4 xl:!w-[30px] h-4 xl:!h-[30px] rounded-full peer-checked:translate-x-5 xl:peer-checked:!translate-x-9 transition-all">
                    </div>
                </label>
            </div>
            <div class="border-b-[3px] border-[#434343] w-full"></div>

            <div class="flex flex-col">
                <p class="text-base md:!text-lg xl:!text-[26px] text-white">Dossier du launcher</p>
                <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">
                    Répertoire des données du launcher.
                </p>
                <div
                    class="mt-[20px] flex items-center gap-2 border border-[#434343] rounded-lg overflow-hidden w-full md:!w-[592px] h-[52px] !px-3">
                    <input type="text" readonly value="C:\Users\AppData\Roaming\Pokeisland Launcher V1"
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
                            <button @click="deleteFile('launcher', index)" class="text-gray-400 text-base md:!text-[24px] hover:text-red-500">
                                <i class="fa-solid fa-trash"></i>
                            </button>
                            <!-- toggle -->
                            <label class="relative inline-flex items-center cursor-pointer">
                                <input type="checkbox" class="sr-only peer" :checked="file.enabled"
                                    @change="toggleFile('launcher', index)" />
                                <div class="w-11 xl:!w-[80px] h-6 xl:!h-[50px] bg-[#434343] rounded-full peer peer-checked:!bg-white transition-all">
                                </div>
                                <div
                                    class="absolute left-1 xl:!left-[8px] top-1 xl:!top-[9px] bg-[#2B2B2B] w-4 xl:!w-[30px] h-4 xl:!h-[30px] rounded-full peer-checked:translate-x-5 xl:peer-checked:!translate-x-9 transition-all">
                                </div>
                            </label>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Dossier du Client -->
            <div class="flex flex-col">
                <p class="text-base md:!text-lg xl:!text-[26px] text-white">Dossier du Client</p>
                <p class="text-xs md:!text-sm xl:!text-[22px] text-[#9D9D9D]">
                    Répertoire des données du client de jeu.
                </p>
                <div
                    class="mt-[20px] flex items-center gap-2 border border-[#434343] rounded-lg overflow-hidden w-full md:!w-[592px] h-[52px] !px-3">
                    <input type="text" readonly value="C:\Users\AppData\Roaming\Pokeisland Launcher V1"
                        class="flex-1 !bg-transparent px-4 py-2 white outline-none cursor-default text-xs md:!text-base" />
                    <label
                        class="bg-[#434343] transition w-[100px] md:!w-[195px] h-[32px] cursor-pointer text-[10px] md:text-base flex justify-center items-center rounded-[10px]">
                        Choisir un fichier
                        <input type="file" class="hidden" multiple @change="(e) => handleFileUpload(e, 'client')" />
                    </label>
                </div>

                <!-- Uploaded client files -->
                <div v-if="clientFiles.length" class="mt-4 flex flex-col gap-3">
                    <div v-for="(file, index) in clientFiles" :key="index"
                        class="flex justify-between items-center bg-[#2B2B2B] rounded-lg px-4 py-3">
                        <div>
                            <p class="font-medium">{{ file.name }}</p>
                            <p class="text-xs text-gray-400">{{ file.version }}</p>
                        </div>
                        <div class="flex items-center gap-3">
                            <!-- delete -->
                            <button @click="deleteFile('client', index)" class="text-gray-400 hover:text-red-500">
                                <i class="fa-solid fa-trash"></i>
                            </button>
                            <!-- toggle -->
                            <label class="relative inline-flex items-center cursor-pointer">
                                <input type="checkbox" class="sr-only peer" :checked="file.enabled"
                                    @change="toggleFile('client', index)" />
                                <div class="w-10 h-5 bg-gray-600 rounded-full peer-checked:bg-[#FFE400] transition-all">
                                </div>
                                <div
                                    class="absolute left-1 top-1 bg-white w-3.5 h-3.5 rounded-full peer-checked:translate-x-5 transition-all">
                                </div>
                            </label>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
/* Custom Scrollbar */
.custom-scroll::-webkit-scrollbar {
    width: 10px;
    /* scrollbar ki motai */
}

.custom-scroll::-webkit-scrollbar-track {
    background: #2c2c2c;
    /* tumhara container jaisa color */
    border-radius: 10px;
}

.custom-scroll::-webkit-scrollbar-thumb {
    background: #ffffff;
    /* white color thumb */
    border-radius: 10px;
}

.custom-scroll::-webkit-scrollbar-thumb:hover {
    background: #d9d9d9;
    /* halka grey hover effect */
}
</style>
