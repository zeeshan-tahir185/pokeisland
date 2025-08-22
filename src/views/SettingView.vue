<script setup>
import { ref, computed } from 'vue'
import Header from '@/components/Header.vue'

// Tabs ke components import karna
import LauncherTab from '@/components/settings/LauncherTab.vue'
import JavaTab from '@/components/settings/JavaTab.vue'
import ModsTab from '@/components/settings/ModsTab.vue'

const activeTab = ref('launcher')

const changeTab = (tab) => {
    activeTab.value = tab
}

// Modal close -> home page redirect
const closeModal = () => {
    window.location.href = '/' // agar vue-router use kar rahe ho to: router.push("/")
}

// Tab switcher mapping
const activeTabComponent = computed(() => {
    switch (activeTab.value) {
        case 'launcher':
            return LauncherTab
        case 'java':
            return JavaTab
        case 'mods':
            return ModsTab
        default:
            return LauncherTab
    }
})
function openLogin(){
      window.location.href = '/login'
}
</script>

<template>
    <div
        class="main-wrapper flex flex-col rounded-[30px] overflow-hidden min-h-[100vh] xl:!min-h-[1000px] px-[20px] md:!px-[5%] max-w-[1920px] md:!mx-auto py-[50px] md:!py-[100px] transition-all duration-700 ease-in-out">
        <Header />
        <div class="relative w-full min-h-[100vh] xl:!min-h-[1000px]">
            <img src="@/assets/setting/bg_setting.png" alt=""
                class="absolute top-0 left-0 w-full h-full object-cover z-0 rounded-br-[30px] rounded-bl-[30px]" />

            <div class="flex items-center min-h-[100vh] xl:!min-h-[1000px] rounded-br-[30px] rounded-bl-[30px] overflow-hidden">
                <div
                    class="rounded-br-[30px] rounded-bl-[30px] bg-transparent z-40 w-full">
                    <!-- Main Section -->
                    <div class="flex min-h-[90vh] xl:!min-h-[900px] w-full md:!w-[95%] 2xl:!w-[1540pxs] mx-5 md:!mx-auto rounded-[30px] border-[3px] border-[#434343] overflow-hidden">
                        <!-- Sidebar -->
                        <div class="w-[70px] sm:!w-[80px] lg:!w-[250px] xl:!w-auto bg-[#2B2B2B] flex flex-col justify-between px-[10px] lg:!px-[30px] !py-[50px] border-r-[3px] border-[#434343]">
                            <!-- Top Tabs -->
                            <div class="flex flex-col gap-4">
                                <button class="text-center lg:!text-left flex justify-center lg:!justify-start items-center xl:!h-[60px] w-full xl:!w-[250px] cursor-pointer text-[10px] lg:!text-[22px] font-semibold poppind lg:!px-5 h-[30px] rounded-[30px]  transition-all" :class="activeTab === 'launcher'
                                        ? 'bg-[#FFE400] text-[#151515]'
                                        : 'text-white hover:bg-gray-700'
                                    " @click="changeTab('launcher')">
                                    Launcher
                                </button>
                                <button class="lg:!text-left flex justify-center lg:!justify-start items-center xl:!h-[60px] w-full xl:!w-[250px] cursor-pointer text-[10px] lg:!text-[22px] font-semibold poppind lg:!px-5 h-[30px] rounded-[30px] text-center transition-all" :class="activeTab === 'java'
                                        ? 'bg-[#FFE400] text-[#151515]'
                                        : 'text-white hover:bg-gray-700'
                                    " @click="changeTab('java')">
                                    Java
                                </button>
                                <button class="lg:!text-left flex justify-center lg:!justify-start items-center xl:!h-[60px] w-full xl:!w-[250px] cursor-pointer text-[10px] lg:!text-[22px] font-semibold poppind lg:!px-5 h-[30px] rounded-[30px] text-center transition-all" :class="activeTab === 'mods'
                                        ? 'bg-[#FFE400] text-[#151515]'
                                        : 'text-white hover:bg-gray-700'
                                    " @click="changeTab('mods')">
                                    Mods
                                </button>
                            </div>

                            <!-- Bottom User Profile -->
                            <div class="flex items-center gap-3 p-3 bg-[#2c2c2c] rounded-lg cursor-pointer flex-col lg:!flex-row" @click="openLogin">
                                <img src="@/assets/setting/profile.svg" alt="profile" class="w-10 2xl:!w-[76px] h-10 2xl:!h-[76px] rounded-md" />
                                <div class="hidden sm:!flex flex-col justify-center lg:!justify-start text-center lg:!text-start">
                                    <p class="text-white text-[8px] lg:!text-base ">TheDiamondMinecart</p>
                                    <p class="text-[7px] lg:!text-[10px] text-[#A7A7A7]">septminecraft@gmail.com</p>
                                    <p class="text-[#6BE500] text-[9px] lg:!text-[10px]">Connecté <i class="fa-regular fa-circle-check"></i></p>
                                </div>
                            </div>
                        </div>

                        <!-- Right Content -->
                        <div class="flex-1 bg-[#222222] p-6 relative">
                            <!-- Close Button -->
                            <button class="absolute top-4 right-4 text-gray-400 hover:text-white text-xl"
                                @click="closeModal">
                                ✕
                            </button>

                            <!-- Dynamic Content -->
                            <component :is="activeTabComponent" />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
