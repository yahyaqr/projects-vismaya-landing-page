<template>
    <section class="bg-teal-500 py-16">
        <div class="container mx-auto px-4 text-center">
            <h2 class="text-3xl sm:text-4xl font-bold mb-6 text-white">
                Ready to Transform Your Business?
            </h2>
            <p class="text-xl mb-8 max-w-2xl mx-auto text-white">
                Let's collaborate to bring your vision to life. Our team of experts is ready to help you achieve your
                goals.
            </p>
            <div class="flex flex-col items-center gap-4">
                <!-- Button -->
                <div class="relative">
                    <button @click="openHireUsModal"
                        class="relative bg-orange-500 text-white px-8 py-4 sm:px-10 sm:py-5 rounded-full text-lg sm:text-xl font-semibold flex items-center justify-center overflow-hidden group transition-all shadow-lg hover:scale-105 w-[200px]"
                        @mouseover="isHovered = true" @mouseleave="isHovered = false">
                        <!-- Gradient Background -->
                        <div
                            class="absolute inset-0 bg-gradient-to-r from-orange-500 to-teal-500 transition-transform duration-500 ease-out transform -translate-x-full group-hover:translate-x-0">
                        </div>

                        <!-- Text Toggle -->
                        <span class="relative z-10">
                            <span v-if="!isHovered">Hire Us Now</span>
                            <span v-else>50% Discount</span>
                        </span>
                    </button>
                </div>
                <!-- Countdown -->
                <p class="text-white text-sm sm:text-base font-medium">
                    Limited Offer Ends In: <strong>{{ countdown }}</strong>
                </p>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

// Props
defineProps(['openHireUsModal']);

// Reactive state for hover effect
const isHovered = ref(false);

// Reactive state for countdown
const countdown = ref('');
let countdownInterval = null;

const startCountdown = () => {
    const targetTime = new Date(Date.now() + 40 * 60 * 1000); // Set target to 40 minutes from now

    const updateCountdown = () => {
        const now = new Date();
        const remainingTime = targetTime - now;

        if (remainingTime <= 0) {
            countdown.value = '00:00:00';
            clearInterval(countdownInterval); // Stop the countdown
            return;
        }

        const minutes = String(Math.floor((remainingTime % (1000 * 60 * 60)) / (1000 * 60))).padStart(2, '0');
        const seconds = String(Math.floor((remainingTime % (1000 * 60)) / 1000)).padStart(2, '0');

        countdown.value = `00:${minutes}:${seconds}`;
    };

    // Update countdown every second
    updateCountdown(); // Initialize countdown immediately
    countdownInterval = setInterval(updateCountdown, 1000);
};

// Lifecycle hooks
onMounted(() => {
    startCountdown();
});

onBeforeUnmount(() => {
    if (countdownInterval) clearInterval(countdownInterval); // Clear interval when component unmounts
});
</script>

<style scoped>
button {
    position: relative;
    font-family: inherit;
    text-transform: capitalize;
}

button:hover {
    transition: transform 0.3s ease-out, box-shadow 0.3s ease-out;
}

button span {
    white-space: nowrap;
    /* Prevent text wrapping */
}
</style>
