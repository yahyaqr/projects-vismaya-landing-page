<template>
    <section class="w-full px-4 py-6 bg-gradient-to-br from-teal-500 to-teal-600">
        <div class="container mx-auto flex flex-col sm:flex-row items-center justify-between">
            <!-- Text Content -->
            <div class="text-left sm:w-1/2">
                <h2 class="text-2xl sm:text-3xl font-bold mb-2 text-white">
                    Transform Your Business
                </h2>
                <p class="text-sm sm:text-base mb-2 text-teal-50">
                    Let's bring your vision to life. Our experts are ready to help.
                </p>
            </div>



            <!-- Button -->
            <div class="relative group sm:w-1/2 max-w-xs w-full">
                <div
                    class="absolute -inset-0.5 bg-gradient-to-r from-orange-400 to-orange-600 rounded-full blur opacity-75 group-hover:opacity-100 transition duration-1000 group-hover:duration-200 animate-pulse">
                </div>
                <button @click="openHireUsModal"
                    class="relative w-full px-4 py-3 bg-orange-500 rounded-full leading-none flex items-center justify-center space-x-2"
                    @mouseover="isHovered = true" @mouseleave="isHovered = false">
                    <ZapIcon :size="20" class="text-white" />
                    <span class="text-white font-semibold text-sm sm:text-base">
                        {{ isHovered ? '50% Discount' : 'Hire Us Now' }}
                    </span>
                </button>
                <!-- Countdown -->
                <div class="text-white text-xs sm:text-sm font-medium flex items-center space-x-2">
                    <ClockIcon :size="16" class="text-orange-200" />
                    <span>Ends in:</span>
                    <span class="font-mono text-orange-100 bg-teal-600 px-2 py-1 rounded-full">{{ countdown }}</span>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { ZapIcon, ClockIcon } from 'lucide-vue-next'

// Props
defineProps(['openHireUsModal'])

// Reactive state for hover effect
const isHovered = ref(false)

// Reactive state for countdown
const countdown = ref('')
let countdownInterval = null

const startCountdown = () => {
    const targetTime = new Date(Date.now() + 40 * 60 * 1000) // Set target to 40 minutes from now

    const updateCountdown = () => {
        const now = new Date()
        const remainingTime = targetTime - now

        if (remainingTime <= 0) {
            countdown.value = '00:00:00'
            clearInterval(countdownInterval) // Stop the countdown
            return
        }

        const minutes = String(Math.floor((remainingTime % (1000 * 60 * 60)) / (1000 * 60))).padStart(2, '0')
        const seconds = String(Math.floor((remainingTime % (1000 * 60)) / 1000)).padStart(2, '0')

        countdown.value = `${minutes}:${seconds}`
    }

    // Update countdown every second
    updateCountdown() // Initialize countdown immediately
    countdownInterval = setInterval(updateCountdown, 1000)
}

// Lifecycle hooks
onMounted(() => {
    startCountdown()
})

onBeforeUnmount(() => {
    if (countdownInterval) clearInterval(countdownInterval) // Clear interval when component unmounts
})
</script>

<style scoped>
.animate-pulse {
    animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes pulse {

    0%,
    100% {
        opacity: 1;
    }

    50% {
        opacity: .5;
    }
}
</style>