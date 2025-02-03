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
    { src: '/clients/berkaslegal.png', alt: 'Berkas Legal', description: 'Legal Competency Training Institute, member of Berkas Amerta Group.' },
    { src: '/clients/ptchc.png', alt: 'PT CHC', description: 'Leading Indonesian steel fabricator specializing in welded H-beams, bridges, and high-rise buildings.' },
    { src: '/clients/iwpc.png', alt: 'IWPC', description: 'A community of Indonesian wedding photographers committed to mutual support and excellence in capturing wedding moments.' },
    { src: '/clients/kmcm.png', alt: 'KMCM', description: 'KMCM Group provides comprehensive eye care services, including consultations, eye examinations, and treatments, with BPJS acceptance.' },
    { src: '/clients/magalarva.png', alt: 'Magalarva', description: 'Indonesian company producing sustainable protein for animal feed by transforming food waste using Black Soldier Fly larvae.' },
    { src: '/clients/sabilamall.png', alt: 'Sabilamall', description: 'Indonesian reseller and dropshipper platform offering a wide range of products from over 50 brands, enabling individuals to start their own businesses.' },
    { src: '/clients/ptsgn.png', alt: 'PT Sumber Guna Nusantara', description: 'Leading supplier and distributor of building finishing materials, including vinyl PVC sheets, carpets, and raised floors.' },
    { src: '/clients/wbaf.png', alt: 'WBAF', description: 'International organization aiming to ease access to finance for businesses from startup to scale-up, fostering economic development globally.' },
    { src: '/clients/ptzulin.png', alt: 'PT Zulin', description: 'Pioneering Indonesian company specializing in formwork and scaffolding solutions for various construction projects.' },
    { src: '/clients/selfashion.png', alt: 'Selfashion', description: 'A startup that enables customers to design and create their own personalized fashion.' },
    { src: '/clients/congen.png', alt: 'Connecting Generations', description: 'A campaign for the election of the FTUI alumni association president.' },
    { src: '/clients/fishcore.png', alt: 'Fishcore', description: 'A startup that helps beginner fish farmers learn biofloc cultivation methods.' },
    { src: '/clients/nyambee.png', alt: 'Nyambee', description: 'A startup that connects micro content creators with corporate clients.' },
    { src: '/clients/streameal.png', alt: 'Streameal', description: 'An MSME business offering food products designed to accompany movie streaming experiences.' },
    { src: '/clients/sajadang.png', alt: 'Sajadang', description: 'An initiative for a business competition focused on transforming waste into money.' },
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