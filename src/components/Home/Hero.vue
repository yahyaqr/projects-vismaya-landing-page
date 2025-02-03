<template>
    <Header />

    <section
        class="container mx-auto px-6 lg:px-20 py-8 flex flex-col-reverse lg:flex-row items-center justify-center gap-6 lg:gap-12">

        <!-- Left Content -->
        <div class="lg:flex-1 max-w-2xl text-center lg:text-left">
            <div>
                <h1 class="text-3xl sm:text-4xl lg:text-6xl font-extrabold leading-tight text-gray-800 mb-6 sm:mb-8">
                    Ready to take business growth<br class="hidden sm:inline" /> to the next level?
                </h1>
                <div class="mb-4 sm:mb-6 leading-relaxed">
                    <p class="text-gray-600 text-base sm:text-lg lg:text-2xl mb-2">
                        Vismaya helps businesses achieve their full potential through innovative digital solutions
                        and strategic growth strategies.
                    </p>
                </div>
            </div>

            <div class="flex flex-col items-center lg:items-start gap-2 sm:gap-4">
                <a href="https://wa.me/+628976075402" target="_blank"
                    class="flex slide-button items-center gap-2 px-8 py-4 sm:px-10 sm:py-5 rounded-lg bg-white border-2 border-green-500 text-green-500 overflow-hidden relative whatsapp-btn">

                    <!-- Default Icon -->
                    <img :src="'src/assets/whatsapp.svg'" class="w-5 h-5 relative z-10 icon-default" />

                    <!-- White Icon (for hover) -->
                    <img :src="'src/assets/whatsapp-white.svg'" class="w-5 h-5 relative z-10 icon-hover" />

                    <span class="relative z-10">Chat With Us</span>
                </a>
            </div>
        </div>

        <!-- Right Illustration -->
        <div class="lg:flex-1 max-w-lg perspective mx-auto sm:mx-0" @mousemove="handleMouseMove"
            @mouseleave="resetTransform">
            <img ref="illustration" src="/src/assets/Hero.png" alt="Hero illustration"
                class="w-64 sm:w-80 lg:w-full max-w-full transform transition-transform duration-300 illustration" />
        </div>
    </section>
</template>

<script setup>
import Header from '../Header.vue';
import { ref } from "vue";

// Reactive state for 3D rotation
const illustration = ref(null);

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

<style scoped>
/* Adding perspective to the parent container */
.perspective {
    perspective: 1000px;
}

.illustration {
    transform-origin: center;
    transition: transform 0.3s ease-out;
}

/* Slide Up Button */
.slide-button::before {
    content: '';
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    height: 100%;
    background: #22c55e;
    transition: all 0.3s;
    z-index: 1;
}

.slide-button:hover::before {
    top: 0;
}

.slide-button:hover {
    color: white;
}

/* WhatsApp Icon Hover Effect */
.icon-hover {
    display: none;
}

.whatsapp-btn:hover .icon-default {
    display: none;
}

.whatsapp-btn:hover .icon-hover {
    display: inline;
}
</style>
