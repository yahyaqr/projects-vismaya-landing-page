<template>
    <section class="w-full px-4 py-4 bg-gray-100">
        <div class="max-w-6xl flex mx-auto items-center">
            <!-- Left Column: Title -->
            <p class="text-sm text-gray-400 font-thin tracking-widest w-32">
                OUR CLIENTS
            </p>

            <!-- Right Column: Carousel Wrapper -->
            <div class="relative flex-1 overflow-hidden">
                <!-- Carousel Items -->
                <div class="flex transition-transform duration-500 ease-in-out"
                    :style="{ transform: `translateX(-${currentIndex * (100 / 6)}%)` }">
                    <div v-for="(client, index) in clients" :key="index"
                        class="client-card w-1/6 flex-shrink-0 p-4 flex items-center justify-center relative transition-all duration-300 group">
                        <!-- Client Logo and Info Container -->
                        <div class="flex items-center w-full h-20 relative cursor-pointer transition-all duration-300">
                            <!-- Client Logo -->
                            <img :src="client.src" :alt="client.alt"
                                class="w-20 h-20 object-contain transition-all duration-300" />

                            <!-- Client Info (Slides out on hover) -->
                            <div
                                class="absolute left-24 w-0 group-hover:w-[calc(100%-6rem)] h-full bg-opacity-95 opacity-0 group-hover:opacity-100 transition-all duration-300 overflow-hidden">
                                <div class="p-2 flex flex-col justify-center h-full">
                                    <h3
                                        class="text-sm font-semibold text-gray-800 whitespace-nowrap overflow-hidden text-ellipsis">
                                        {{ client.alt }}
                                    </h3>
                                    <p class="text-xs text-gray-600 leading-snug mt-1 overflow-hidden">
                                        {{ client.description }}
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const clients = [
    { src: '/clients/berkaslegal.png', alt: 'Berkas Legal', description: 'Providing digital marketing strategies.' },
    { src: '/clients/ptchc.png', alt: 'PT CHC', description: 'Custom software development solutions.' },
    { src: '/clients/congen.png', alt: 'Connecting Generations', description: 'Innovative e-commerce solutions.' },
    { src: '/clients/fishcore.png', alt: 'Fishcore', description: 'UX/UI design services for better engagement.' },
    { src: '/clients/iwpc.png', alt: 'IWPC', description: 'Cloud infrastructure management support.' },
    { src: '/clients/kmcm.png', alt: 'KMCM', description: 'Mobile app development for seamless user experience.' },
    { src: '/clients/magalarva.png', alt: 'Magalarva', description: 'Comprehensive cybersecurity solutions.' },
    { src: '/clients/nyambee.png', alt: 'Nyambee', description: 'Data analytics and business insights services.' },
    { src: '/clients/sabilamall.png', alt: 'Sabilamall', description: 'Innovative marketplace solutions for retailers.' },
    { src: '/clients/sajadang.png', alt: 'Sajadang', description: 'Supply chain optimization and automation.' },
    { src: '/clients/selfashion.png', alt: 'Selfashion', description: 'Fashion e-commerce platform development.' },
    { src: '/clients/ptsgn.png', alt: 'PT SGN', description: 'Next-gen digital transformation strategies.' },
    { src: '/clients/streameal.png', alt: 'Streameal', description: 'On-demand streaming and media solutions.' },
    { src: '/clients/WBAF.png', alt: 'WBAF', description: 'Financial technology and advisory services.' },
    { src: '/clients/ptzulin.png', alt: 'PT Zulin', description: 'AI-powered customer engagement solutions.' }
];

const currentIndex = ref(0);
let autoScrollInterval;

const startAutoScroll = () => {
    autoScrollInterval = setInterval(() => {
        currentIndex.value = (currentIndex.value + 1) % (clients.length - 5); // Adjust for 5 visible items
    }, 3000);
};

const stopAutoScroll = () => {
    clearInterval(autoScrollInterval);
};

onMounted(() => {
    startAutoScroll();
});

onUnmounted(() => {
    stopAutoScroll();
});
</script>

<style scoped>
.client-card {
    transition: all 0.3s ease;
}

.client-card:hover {
    width: 35% !important;
}

.client-card:hover~.client-card {
    width: 13% !important;
}
</style>