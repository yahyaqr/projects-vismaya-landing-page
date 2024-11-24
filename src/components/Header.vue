<template>
    <header class="container mx-auto px-4 py-4 sm:py-6">
        <!-- Navbar -->
        <nav class="flex justify-between items-center">
            <!-- Logo -->
            <div class="flex items-center space-x-3">
                <img src="../assets/Logo.png" alt="Vismaya Lab Logo" class="w-10 h-10" />
                <span class="font-semibold text-teal-500 text-lg">Vismaya Lab</span>
            </div>

            <!-- Desktop Menu -->
            <div class="hidden md:flex items-center space-x-6">
                <a href="/portfolio" class="text-gray-800 hover:text-teal-500 transition-colors text-base font-medium">
                    Our Portfolio
                </a>
                <!-- Hire Us Button with Text Change and Animation -->
                <div class="relative">
                    <button @click="openHireUsModal"
                        class="relative bg-orange-500 text-white px-2 py-2 rounded-full text-base font-medium flex items-center justify-center overflow-hidden group transition-all shadow-lg hover:scale-105 w-[140px]"
                        @mouseover="isHovered = true" @mouseleave="isHovered = false">
                        <!-- Gradient Background -->
                        <div
                            class="absolute inset-0 bg-gradient-to-r from-orange-500 to-teal-500 transition-transform duration-500 ease-out transform -translate-x-full group-hover:translate-x-0">
                        </div>
                        <!-- Button Text -->
                        <span class="relative z-10">
                            <span v-if="!isHovered">Hire Us</span>
                            <span v-else>50% Discount</span>
                        </span>
                    </button>
                </div>
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
            <a href="/portfolio"
                class="block w-full text-left py-2 px-4 text-sm text-gray-800 hover:bg-gray-100 rounded transition-colors">
                Our Portfolio
            </a>
            <button @click="openHireUsModal"
                class="block w-full text-left py-2 px-4 text-sm text-gray-800 hover:bg-gray-100 rounded transition-colors">
                Hire Us
            </button>
        </div>
    </header>
</template>

<script setup>
import { ref } from "vue";
import { Menu, X } from "lucide-vue-next";

defineProps(["openHireUsModal"]);

const mobileMenuOpen = ref(false);
const isHovered = ref(false);

const toggleMobileMenu = () => {
    mobileMenuOpen.value = !mobileMenuOpen.value;
};
</script>

<style>
/* Button Styling */
button {
    position: relative;
    font-family: inherit;
    text-transform: capitalize;
    width: 140px;
    /* Fixed width to ensure consistent size on hover */
}

button span {
    white-space: nowrap;
    /* Prevent text wrapping */
}

button:hover {
    transition: transform 0.3s ease-out, box-shadow 0.3s ease-out;
}
</style>