<template>
    <section class="relative text-white py-16 px-4 sm:py-20 sm:px-6 md:px-8">
        <div class="mx-auto w-full px-4 sm:px-6">
            <div class="flex flex-col py-10 lg:py-16 gap-8 sm:gap-10 md:gap-12 lg:gap-20">
                <!-- Heading -->
                <h2
                    class="font-playfair text-white tracking-tight text-3xl sm:text-4xl md:text-5xl leading-tight text-center">
                    Our Satisfied Partners
                </h2>

                <!-- Logo Cloud -->
                <div class="flex flex-wrap justify-center items-center gap-6">
                    <component v-for="(logo, index) in partnerLogos" :key="index" :is="logo.link ? 'a' : 'div'"
                        :href="logo.link || null" target="_blank" rel="noopener" :class="[
                        'flex items-center justify-center max-w-[120px] max-h-[80px] w-full h-full p-2 rounded-md transition-transform hover:scale-105',
                        logo.whiteBg ? 'bg-white' : ''
                    ]" @mouseenter="hoveredIndex = index" @mouseleave="hoveredIndex = null">
                        <img :src="logo.src" :alt="logo.alt"
                            :class="['object-contain max-w-full max-h-full', logo.invert ? 'invert' : '']" />
                    </component>
                </div>


                <!-- After the logo grid -->
                <div class="w-full pt-4 text-center text-base font-medium text-white min-h-[2.5rem] transition-all duration-200"
                    style="min-height:2.5rem;">
                    <span :class="[
                        'bg-black bg-opacity-50 rounded px-4 py-2 inline-block shadow transition-opacity duration-200 leading-relaxed font-light',
                        hoveredIndex !== null ? 'opacity-100' : 'opacity-0 pointer-events-none'
                    ]" style="transition:opacity 0.2s;">
                        {{ hoveredIndex !== null
                        ? partnerLogos[hoveredIndex].alt + ': ' + partnerLogos[hoveredIndex].description
                        : '\u00A0' }}
                    </span>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue';

const hoveredIndex = ref(null);

const partnerLogos = ref([
    { src: '/src/assets/clients-2/berkaslegal.png', invert: false, whiteBg: true, alt: 'Berkas Legal', description: 'Legal competency training institute.', link: 'https://www.instagram.com/berkas_legal/', },
    { src: '/src/assets/clients-2/congen.png', invert: false, whiteBg: true, alt: 'Connecting Generations', description: 'FTUI alumni election campaign.', link: 'https://connectinggenerations.netlify.app/', },
    { src: '/src/assets/clients-2/fishcore.png', invert: false, whiteBg: true, alt: 'Fishcore', description: 'Biofloc fish farming learning platform.', link: 'https://www.fishcore.id/', },
    { src: '/src/assets/clients-2/iwpc.png', invert: false, whiteBg: true, alt: 'IWPC', description: 'Community of Indonesian wedding photographers.', link: 'https://www.instagram.com/iwpc.id/', },
    { src: '/src/assets/clients-2/kmcm.png', invert: false, whiteBg: true, alt: 'KMCM', description: 'Comprehensive eye care service provider.', link: 'https://www.instagram.com/klinikmatacibinongmedika/', },
    { src: '/src/assets/clients-2/magalarva.png', invert: false, whiteBg: true, alt: 'Magalarva', description: 'Sustainable protein producer from food waste.', link: 'https://www.instagram.com/magalarva/', },
    { src: '/src/assets/clients-2/nyambee.png', invert: false, whiteBg: true, alt: 'Nyambee', description: 'Platform connecting creators with clients.', link: 'https://www.instagram.com/nyambee_official/', },
    { src: '/src/assets/clients-2/ptchc.png', invert: false, whiteBg: true, alt: 'PT CHC', description: 'Steel fabricator for construction projects.', link: 'https://cigading-habeam.com/', },
    { src: '/src/assets/clients-2/ptsgn.png', invert: false, whiteBg: true, alt: 'PT Sumber Guna Nusantara', description: 'Supplier of building finishing materials.', link: 'https://sumbergunanusantara.co.id/', },
    { src: '/src/assets/clients-2/ptzulin.png', invert: false, whiteBg: true, alt: 'PT Zulin', description: 'Formwork and scaffolding solutions provider.', link: 'https://zulin.co.id/', },
    { src: '/src/assets/clients-2/sabilamall.png', invert: false, whiteBg: true, alt: 'Sabilamall', description: 'Reseller and dropshipper platform in Indonesia.', link: 'https://www.sabilamall.co.id/', },
    { src: '/src/assets/clients-2/sajadang.png', invert: false, whiteBg: true, alt: 'Sajadang', description: 'Competition to turn waste into money.', },
    { src: '/src/assets/clients-2/selfashion.png', invert: false, whiteBg: true, alt: 'Selfashion', description: 'Custom fashion design startup.', },
    { src: '/src/assets/clients-2/streameal.png', invert: false, whiteBg: true, alt: 'Streameal', description: 'Food business for movie streaming.', link: 'https://www.instagram.com/streameal/', },
    { src: '/src/assets/clients-2/wbaf.png', invert: false, whiteBg: true, alt: 'WBAF', description: 'Global organization supporting business finance.', link: 'https://www.instagram.com/angelsweek.id/', },
]);

// const partnerLogos = ref([
//     { src: '/src/assets/clients/1-ibiza.png', invert: false },
//     { src: '/src/assets/clients/2-krispy.png', invert: false },
//     { src: '/src/assets/clients/3-uniqlo.png', invert: false },
//     { src: '/src/assets/clients/4-atome.png', invert: false },
//     { src: '/src/assets/clients/5-tanamera.png', invert: false },
//     { src: '/src/assets/clients/6-hsbc.png', invert: false },
//     { src: '/src/assets/clients/7-pertamina.png', invert: false },
//     { src: '/src/assets/clients/8-kai.png', invert: false },
//     { src: '/src/assets/clients/9-nyu.png', invert: false },
//     { src: '/src/assets/clients/10-wuling.png', invert: false },
//     { src: '/src/assets/clients/11-3ce.png', invert: true },
//     { src: '/src/assets/clients/12-tmii.png', invert: false },
//     { src: '/src/assets/clients/13-suko.png', invert: false },
//     { src: '/src/assets/clients/14-kasual.png', invert: false }
// ]);
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.2s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

.fade-enter-to,
.fade-leave-from {
    opacity: 1;
}
</style>
