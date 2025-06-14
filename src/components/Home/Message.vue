<template>
    <section class="w-full h-full flex justify-center overflow-hidden relative">
        <!-- Closed Envelope (only before opening) -->
        <img v-if="!animationStarted" src="/src/assets/closed-envelope.png" alt="Closed Envelope" class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2
        w-auto h-auto max-w-[90%] md:max-w-[780px] xl:max-w-[1100px] z-20 pointer-events-none">

        <button v-if="!animationStarted" @click="startAnimation" class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 z-30
               bg-[#11A8AB] hover:bg-[#11a1a3] text-white font-inter font-bold py-3 px-6 rounded-lg
               transition-all duration-300 shadow-lg hover:shadow-xl text-lg pointer-events-auto font-sans">
            Open Envelope
        </button>

        <!-- Letter Container (hidden before animation) -->
        <div v-show="animationStarted" class="relative w-full max-w-6xl h-full">
            <!-- Back Envelope -->
            <div class="absolute inset-0 w-full h-full transition-transform duration-700 ease-out z-10"
                :style="{ transform: `translateY(${envelopeY}px)` }">
                <img src="/src/assets/back-envelope.png" alt="Back Envelope"
                    class="absolute inset-0 w-full h-auto object-contain" />
            </div>

            <!-- Paper -->
            <div class="absolute inset-0 w-full transition-transform duration-700 ease-out z-20"
                :style="{ transform: `translateY(${paperY}px)` }">
                <img src="/src/assets/paper.png" alt="Paper" class="w-full h-auto object-contain" />
                <div class="absolute inset-0 pt-8 sm:pt-20 lg:pt-40 px-4 sm:px-10 lg:px-20
                       flex flex-col justify-start items-center text-center gap-y-6 w-full">
                    <div class="w-full max-w-[95%] px-8 text-left">
                        <h1
                            class="text-center text-xl sm:text-2xl lg:text-4xl font-bold text-gray-800 mb-3 lg:mb-8 leading-tight whitespace-nowrap font-playfair">
                            Dear Entrepreneurs,
                        </h1>

                        <p
                            class="text-base sm:text-xl lg:text-2xl text-gray-700 leading-relaxed mb-3 lg:mb-8 whitespace-normal">
                            We know you've got ideas. Big ones. Smart ones. Maybe even brilliant ones.
                            But ideas alone don't grow businesses. Endless planning won't pay the bills.
                            At some point, you've got to launch the product, post the content, run the ads — and start
                            earning.
                        </p>

                        <p class="text-base sm:text-xl lg:text-2xl text-gray-700 leading-relaxed whitespace-normal">
                            That's where we come in. Vismaya helps Entrepreneurs like you turn plans into real results.
                            No fluff. No endless revisions. Just clean execution and digital solutions that move you
                            forward.
                            Because growth doesn't come from thinking — <span
                                class="font-bold italic whitespace-nowrap">
                                it comes from doing.
                            </span>
                        </p>


                    </div>

                </div>
            </div>

            <!-- Front Envelope -->
            <div class="absolute inset-0 w-full h-full transition-transform duration-700 ease-out z-30"
                :style="{ transform: `translateY(${envelopeY}px)` }">
                <img src="/src/assets/front-envelope.png" alt="Front Envelope"
                    class="absolute inset-0 w-full h-auto object-contain pointer-events-none" />
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

// Animation state
const paperY = ref(0);
const envelopeY = ref(0);
const animationStarted = ref(false);

// Responsive animation values
let PAPER_START, PAPER_END, ENVELOPE_END;
const ANIMATION_DURATION = 1500; // in milliseconds

// Animation timing
let animationStartTime = 0;
let animationFrame = null;

const setResponsiveOffsets = () => {
    const width = window.innerWidth;

    if (width < 640) {
        // Mobile
        PAPER_START = 600;
        PAPER_END = 30;
        ENVELOPE_END = 100;
    } else if (width < 1024) {
        // Tablet
        PAPER_START = 800;
        PAPER_END = 70;
        ENVELOPE_END = 300;
    } else {
        // Desktop
        PAPER_START = 900;
        PAPER_END = 100;
        ENVELOPE_END = 300;
    }

    paperY.value = PAPER_START;
    envelopeY.value = 0;
};

const updateOffsetsOnResize = () => {
    const width = window.innerWidth;

    if (width < 640) {
        PAPER_END = 30;
        ENVELOPE_END = 100;
    } else if (width < 1024) {
        PAPER_END = 70;
        ENVELOPE_END = 300;
    } else {
        PAPER_END = 100;
        ENVELOPE_END = 300;
    }

    if (animationStarted.value) {
        paperY.value = PAPER_END;
        envelopeY.value = ENVELOPE_END;
    }
};

const startAnimation = () => {
    animationStarted.value = true;
    animationStartTime = Date.now();

    // Start the animation loop
    animateEnvelope();
};

const animateEnvelope = () => {
    const elapsed = Date.now() - animationStartTime;
    const progress = Math.min(elapsed / ANIMATION_DURATION, 1);

    // Easing function for smoother animation
    const easeOutCubic = t => 1 - Math.pow(1 - t, 3);
    const easedProgress = easeOutCubic(progress);

    // Calculate current positions
    paperY.value = PAPER_START - (PAPER_START - PAPER_END) * easedProgress;
    envelopeY.value = ENVELOPE_END * easedProgress;

    if (progress < 1) {
        animationFrame = requestAnimationFrame(animateEnvelope);
    }
};

onMounted(() => {
    setResponsiveOffsets();
    window.addEventListener('resize', updateOffsetsOnResize);
});

onBeforeUnmount(() => {
    window.removeEventListener('resize', updateOffsetsOnResize);
});
</script>

<style scoped></style>