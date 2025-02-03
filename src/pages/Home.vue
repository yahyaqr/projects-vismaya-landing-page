<template>
    <div class="text-gray-800 font-sans">
        <HeroSection :openHireUsModal="openHireUsModal" />

        <PartnersSection />

        <ServicesSection />

        <AboutSection />

        <ShowcaseSection />

        <TestimonialsSection />

        <CallToActionSection :openHireUsModal="openHireUsModal" />

        <Footer />

        <!-- Modal -->
        <transition name="fade">
            <div v-if="showHireUsModal"
                class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50"
                @keydown.esc="handleKeydown" tabindex="0">
                <!-- Modal Backdrop -->
                <div class="absolute inset-0" @click="closeHireUsModal"></div>

                <!-- Modal Content -->
                <div class="bg-white rounded-lg p-8 max-w-md w-full relative z-10" ref="modalContent">
                    <RPS />
                </div>
            </div>
        </transition>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Importing the modularized components
import HeroSection from '../components/Hero.vue';
import PartnersSection from '../components/Partners.vue';
import ServicesSection from '../components/Services.vue';
import AboutSection from '../components/About.vue';
import ProcessSection from '../components/Process.vue';
import TestimonialsSection from '../components/Testimonials/index.vue';
import ShowcaseSection from '../components/Showcase.vue';
import CallToActionSection from '../components/CTA.vue';
import RPS from '../components/RPS.vue';
import Footer from '../components/Footer.vue';

// State management for the modal
const showHireUsModal = ref(false);

// Open and close modal methods
const openHireUsModal = () => {
    showHireUsModal.value = true;
    console.log('Modal opened!');
};

const closeHireUsModal = () => {
    showHireUsModal.value = false;
    console.log('Modal closed!');
};

// Close modal on Escape key
const handleKeydown = (event) => {
    if (event.key === 'Escape') {
        closeHireUsModal();
    }
};

// Focus management for the modal content
const modalContent = ref(null);
onMounted(() => {
    if (modalContent.value) {
        modalContent.value.focus();
    }
});
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
