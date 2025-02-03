<template>
    <header class="container mx-auto px-4 py-4 sm:py-6">
        <!-- Navbar -->
        <nav class="flex justify-between items-center">
            <!-- Logo -->
            <div class="flex items-center space-x-3">
                <img src="../assets/Logo.png" alt="Vismaya Lab Logo" class="w-10 h-10" />
                <span class="font-semibold text-teal-500 text-2xl">VISMAYA</span>
            </div>

            <!-- Desktop Menu -->
            <div class="hidden md:flex items-center space-x-6">
                <!-- <a href="/portfolio" class="text-gray-800 hover:text-teal-500 transition-colors text-base font-medium">
                    Our Portfolio
                </a> -->
                <!-- Hire Us Button with Text Change and Animation -->
                <a href="https://wa.me/+628976075402" target="_blank"
                    class="flex items-center gap-2 px-6 py-2 rounded-full bg-green-500 text-white hover:bg-green-600 transition-colors duration-300 pulse-animation">
                    <img :src="'src/assets/whatsapp-white.svg'" class="w-5 h-5" />
                    <span>Message Us</span>
                </a>
            </div>

            <!-- Mobile Menu Button -->
            <div class="md:hidden">
                <button @click="toggleMobileMenu" class="text-gray-800 focus:outline-none">
                    <Menu v-if="!mobileMenuOpen" class="w-6 h-6" />
                    <X v-else class="w-6 h-6" />
                </button>
            </div>
        </nav>

        <!-- Mobile Menu -->
        <div v-if="mobileMenuOpen" class="md:hidden mt-4 space-y-2">
            <!-- <a href="/portfolio"
                class="block w-full text-left py-2 px-4 text-sm text-gray-800 hover:bg-gray-100 rounded transition-colors">
                Our Portfolio
            </a> -->
            <a href="https://wa.me/+628976075402" target="_blank"
                class="flex items-center gap-2 px-6 py-2 rounded-full bg-green-500 text-white hover:bg-green-600 transition-colors duration-300 pulse-animation">
                <img :src="'src/assets/whatsapp-white.svg'" class="w-5 h-5" />
                <span>Message Us</span>
            </a>
        </div>
    </header>
</template>

<script setup>
import { ref } from "vue";
import { Menu, X } from "lucide-vue-next";

defineProps(["openHireUsModal"]);

const mobileMenuOpen = ref(false);

const toggleMobileMenu = () => {
    mobileMenuOpen.value = !mobileMenuOpen.value;
};
</script>

<style>
.pulse-animation {
    animation: pulse 2s infinite;
}

@keyframes pulse {
    0% {
        box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.4);
    }

    70% {
        box-shadow: 0 0 0 10px rgba(34, 197, 94, 0);
    }

    100% {
        box-shadow: 0 0 0 0 rgba(34, 197, 94, 0);
    }
}
</style>