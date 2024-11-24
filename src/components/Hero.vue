<template>
    <section
        class="container mx-auto px-6 lg:px-20 py-12 sm:py-16 lg:py-28 flex flex-col-reverse lg:flex-row items-center justify-center gap-6 lg:gap-12">
        <!-- Left Content -->
        <div class="lg:flex-1 max-w-2xl text-center lg:text-left">
            <div>
                <h1 class="text-3xl sm:text-4xl lg:text-6xl font-extrabold leading-tight text-gray-800 mb-6 sm:mb-8">
                    Ready to take business growth<br class="hidden sm:inline" /> to the next level?
                </h1>
                <p class="text-gray-600 text-base sm:text-lg lg:text-2xl mb-8 sm:mb-10 leading-relaxed">
                    Vismaya Lab helps businesses achieve their full potential through innovative digital solutions and
                    strategic
                    growth strategies. <span class="text-orange-500 font-semibold">Limited time discounts
                        available!</span>
                </p>
            </div>
            <div class="flex flex-col items-center lg:items-start gap-2 sm:gap-4">
                <!-- Hire Us Button -->
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
                <p class="text-gray-500 text-sm sm:text-base font-medium text-center lg:text-left">
                    Limited Offer Ends In: <strong>{{ countdown }}</strong>
                </p>
            </div>
        </div>

        <!-- Right Illustration -->
        <div class="lg:flex-1 max-w-lg perspective mx-auto sm:mx-0" @mousemove="handleMouseMove"
            @mouseleave="resetTransform">
            <img ref="illustration" src="../assets/Hero.png" alt="Hero illustration"
                class="w-64 sm:w-80 lg:w-full max-w-full transform transition-transform duration-300 illustration" />
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

// Props
defineProps(["openHireUsModal"]);

// Reactive state for countdown and hover effect
const illustration = ref(null);
const countdown = ref("");
const isHovered = ref(false);

// Countdown logic
let countdownInterval = null;

const startCountdown = () => {
    const targetTime = new Date(Date.now() + 40 * 60 * 1000); // Set target to 40 minutes from now

    const updateCountdown = () => {
        const now = new Date();
        const remainingTime = targetTime - now;

        if (remainingTime <= 0) {
            countdown.value = "00:00:00";
            clearInterval(countdownInterval); // Stop the countdown
            return;
        }

        const minutes = String(Math.floor((remainingTime % (1000 * 60 * 60)) / (1000 * 60))).padStart(2, "0");
        const seconds = String(Math.floor((remainingTime % (1000 * 60)) / 1000)).padStart(2, "0");

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

// 3D Rotation for the illustration
const handleMouseMove = (event) => {
    const bounds = event.currentTarget.getBoundingClientRect();
    const x = event.clientX - bounds.left;
    const y = event.clientY - bounds.top;

    const centerX = bounds.width / 2;
    const centerY = bounds.height / 2;

    const rotateX = ((y - centerY) / centerY) * 15;
    const rotateY = ((x - centerX) / centerX) * -15;

    illustration.value.style.transform = `rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.1)`;
};

const resetTransform = () => {
    illustration.value.style.transform = "rotateX(0deg) rotateY(0deg) scale(1)";
};
</script>


<style>
/* Adding perspective to the parent container */
.perspective {
    perspective: 1000px;
    /* Creates a 3D perspective */
}

.illustration {
    transform-origin: center;
    /* Keep the rotation centered */
    transition: transform 0.3s ease-out;
    /* Smooth rotation reset */
}

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