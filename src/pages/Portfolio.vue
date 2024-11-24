<template>
    <div class="bg-white min-h-screen text-gray-800 font-sans">
        <!-- Pass openHireUsModal to components that need it -->
        <Header :openHireUsModal="openHireUsModal" />

        <Portfolio />

        <Footer />

        <HireUsModal v-if="showHireUsModal" :closeHireUsModal="closeHireUsModal" />
    </div>
</template>

<script setup>
import { ref } from 'vue';

// Importing the modularized components
import Header from '../components/Header.vue';
import Portfolio from '../components/Portfolio.vue';
import Footer from '../components/Footer.vue';
import HireUsModal from '../components/HireUs.vue';


// State management for the modal
const showHireUsModal = ref(false);

const openHireUsModal = () => {
    showHireUsModal.value = true;
};

const closeHireUsModal = () => {
    showHireUsModal.value = false;
};
</script>