<template>
    <div class="text-gray-800 font-sans">
        <HeroSection />

        <ClientsSection />

        <ServicesSection />

        <AboutSection />

        <!-- <ShowcaseSection /> -->

        <TestimonialsSection />

        <CTASection />

        <Footer />
    </div>
</template>

<script setup>
// Importing the modularized components
import HeroSection from '../components/Home/Hero.vue';
import ClientsSection from '../components/Home/Clients.vue';
import ServicesSection from '../components/Home/Services/Index.vue';
import AboutSection from '../components/Home/About.vue';
import TestimonialsSection from '../components/Home/Testimonials/Index.vue';
import ShowcaseSection from '../components/Home/Showcase.vue';
import CTASection from '../components/Home/CTA.vue';
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
