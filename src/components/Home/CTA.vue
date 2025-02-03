<template>
    <section class="w-full px-4 py-6 bg-gradient-to-br from-teal-500 to-teal-600">
        <div class="container mx-auto flex flex-col sm:flex-row items-center justify-between gap-4">
            <!-- Text Content -->
            <div class="text-left sm:w-1/2">
                <h2 class="text-2xl sm:text-3xl font-bold mb-2 text-white">
                    Transform Your Business
                </h2>
                <p class="text-sm sm:text-base mb-2 text-teal-50">
                    Let's bring your vision to life. Our experts are ready to help.
                </p>
            </div>

            <!-- Button and Countdown -->
            <div class="sm:w-1/2 max-w-xs w-full flex flex-col items-center gap-2">
                <!-- Button -->
                <a href="https://wa.me/+628976075402" target="_blank"
                    class="flex justify-center items-center gap-2 w-full px-6 py-3 rounded-full bg-green-500 text-white hover:bg-green-600 transition-colors duration-300 pulse-animation">
                    <img :src="'src/assets/whatsapp-white.svg'" class="w-5 h-5" />
                    <span class="text-white font-semibold text-base sm:text-lg">Message Us</span>
                </a>
            </div>
        </div>
    </section>
</template>

<script setup>
</script>

<style scoped>
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