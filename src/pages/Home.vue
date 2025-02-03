<template>
    <div class="text-gray-800 font-sans">
        <HeroSection />

        <ClientsSection />

        <ServicesSection />

        <AboutSection />

        <!-- <ShowcaseSection /> -->

        <TestimonialsSection />

        <CallToActionSection />

        <Footer />
    </div>
</template>

<script setup>
// Importing the modularized components
import HeroSection from '../components/Hero.vue';
import ClientsSection from '../components/Clients.vue';
import ServicesSection from '../components/Services/Index.vue';
import AboutSection from '../components/About.vue';
import TestimonialsSection from '../components/Testimonials/index.vue';
import ShowcaseSection from '../components/Showcase.vue';
import CallToActionSection from '../components/CTA.vue';
import Footer from '../components/Footer.vue';
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
