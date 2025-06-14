<template>
    <section class="relative text-white p-12 sm:py-24 sm:px-6 md:px-8" aria-label="Creative Carousel">
        <div class="mx-auto w-full px-4 sm:px-6">
            <div class="flex flex-col transition-colors gap-8 lg:gap-12">
                <!-- Header -->
                <div class="flex flex-col px-6 lg:px-20 lg:flex-row lg:items-end lg:justify-between">
                    <div class="flex-col flex gap-2 lg:gap-4 max-w-[360px] lg:max-w-[720px] xl:max-w-[924px] mx-auto">
                        <h2
                            class="font-serif text-white tracking-tight text-3xl sm:text-4xl md:text-5xl leading-tight text-center">
                            Every type of creative work you'll ever need
                        </h2>
                    </div>
                </div>

                <!-- Splide Carousel -->
                <Splide class="splide" :options="splideOptions" ref="splideRef" @splide:moved="onSlideMoved"
                    @splide:mounted="onSlideMounted">
                    <SplideSlide v-for="(card, index) in cards" :key="index" role="group"
                        :aria-label="`Slide ${index + 1} of ${cards.length}`" class="carousel__slide flex">
                        <div class="group relative transition-all duration-700 hover:-translate-y-[5px] lg:hover:-translate-y-[10px] bg-gray-800  overflow-hidden h-[600px] w-[420px] flex-shrink-0"
                            :class="isSlideActive(index) ? 'shadow-2xl scale-105 z-30' : 'z-10'">
                            <!-- Image -->
                            <div class="absolute inset-0">
                                <img :src="card.image" :alt="card.titleNormal"
                                    class="w-full h-full object-cover object-center group-hover:scale-[102%] transition-transform duration-700"
                                    @error="handleImageError" />
                            </div>

                            <!-- Content -->
                            <div class="relative z-20 flex h-full w-[full] flex-col min-h-[300px] sm:min-h-[350px]">
                                <div class="flex flex-col w-full mt-5 sm:mt-0 p-5 text-center sm:group-hover:mt-5 transition-[margin] duration-700"
                                    :class="isSlideActive(index) ? 'sm:mt-2' : ''">
                                    <h4
                                        class="font-serif text-white font-bold tracking-tight text-3xl lg:text-4xl xl:text-5xl leading-tight">
                                        <span v-if="card.titleItalic" class="font-serif italic font-normal">
                                            {{ card.titleItalic }}
                                        </span>
                                        <span>{{ card.titleNormal }}</span>
                                    </h4>
                                </div>

                                <!-- Tags -->
                                <div v-if="card.tags?.length"
                                    class="mt-auto w-full flex flex-wrap gap-1 p-3 opacity-0 group-hover:opacity-100 transition-opacity duration-700"
                                    style="background: linear-gradient(180deg, rgba(0,0,0,0) 0%, rgba(0,0,0,0.25) 100%)">
                                    <span v-for="(tag, ti) in getVisibleTags(card.tags)" :key="ti"
                                        class="text-white text-[10px] px-2 py-0.5 border border-white/50 bg-black/20 rounded-full font-semibold">
                                        {{ tag }}
                                    </span>
                                    <span v-if="card.tags.length > visibleTagCount"
                                        class="text-white text-[10px] px-2 py-0.5 border border-white/50 bg-black/20 rounded-full font-semibold">
                                        +{{ card.tags.length - visibleTagCount }} more
                                    </span>
                                </div>
                            </div>
                        </div>
                    </SplideSlide>
                </Splide>

                <!-- Custom Nav Dots -->
                <div class="flex justify-center gap-1.5 carousel__navdots" role="group"
                    aria-label="Choose slide to display">
                    <button v-for="(card, index) in cards" :key="index"
                        class="h-2 rounded-full transition-all duration-300 cursor-pointer"
                        :class="activeIndex === index ? 'bg-white w-6' : 'bg-gray-400 w-2 hover:bg-gray-300'"
                        @click="goToSlide(index)" :aria-label="`Go to slide ${index + 1}`"
                        :aria-pressed="activeIndex === index" type="button" />
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import '@splidejs/splide/dist/css/splide.min.css';
import { ref, computed, onMounted } from 'vue';
import { Splide, SplideSlide } from '@splidejs/vue-splide';

// Card data
const cards = ref([
    {
        titleItalic: 'Ad ',
        titleNormal: 'Creative',
        subtitle: 'Scroll-stopping visuals for ads that convert.',
        image: '/portfolio/Ad Creative.png',
        tags: ['ads', 'digital marketing', 'creative']
    },
    {
        titleItalic: 'Website ',
        titleNormal: 'Design',
        subtitle: 'Custom layouts that blend function with aesthetic.',
        image: '/portfolio/Website Design.png',
        tags: ['UI/UX', 'responsive', 'landing page']
    },
    {
        titleItalic: 'Social ',
        titleNormal: 'Media',
        subtitle: 'Visual storytelling crafted for Instagram, TikTok, and more.',
        image: '/portfolio/Social Media Creative.png',
        tags: ['content', 'Instagram', 'TikTok']
    },
    {
        titleItalic: 'Email ',
        titleNormal: 'Design',
        subtitle: 'Campaign-ready email layouts that boost open rates.',
        image: '/portfolio/Email Design.png',
        tags: ['newsletter', 'email marketing', 'CRM']
    },
    {
        titleItalic: 'Motion ',
        titleNormal: 'Design',
        subtitle: 'Dynamic motion graphics for digital campaigns.',
        image: '/portfolio/Motion Design.png',
        tags: ['animation', 'video', 'reels']
    },
    {
        titleItalic: 'Video ',
        titleNormal: 'Production',
        subtitle: 'End-to-end video creation tailored to your message.',
        image: '/portfolio/Video Production.png',
        tags: ['shooting', 'editing', 'script']
    },
    {
        titleItalic: 'Marketing ',
        titleNormal: 'Strategy',
        subtitle: 'Data-driven plans to win attention and conversions.',
        image: '/portfolio/Marketing Strategy.png',
        tags: ['growth', 'positioning', 'funnel']
    },
    {
        titleItalic: 'Presentation ',
        titleNormal: 'Design',
        subtitle: 'Investor-ready decks and slides that impress.',
        image: '/portfolio/Presentation Design.png',
        tags: ['pitch deck', 'slides', 'corporate']
    },
    {
        titleItalic: 'Illustration ',
        titleNormal: 'Design',
        subtitle: 'Custom artwork for product, branding, or editorial use.',
        image: '/portfolio/Illustration Design.png',
        tags: ['hand-drawn', 'vector', 'digital art']
    },
    {
        titleItalic: 'AI-Enhanced ',
        titleNormal: 'Creative',
        subtitle: 'Futuristic visuals crafted with generative AI.',
        image: '/portfolio/AI-Enhanced Creative.png',
        tags: ['AI art', 'midjourney', 'innovation']
    },
    {
        titleItalic: 'Packaging & Merch ',
        titleNormal: 'Design',
        subtitle: 'Sell more with standout product and merch packaging.',
        image: '/portfolio/Packaging & Merch Design.png',
        tags: ['label', 'mockup', 'ecommerce']
    },
    {
        titleItalic: 'Brand ',
        titleNormal: 'Identity',
        subtitle: 'Logo, typography, and full brand guidelines.',
        image: '/portfolio/Brand Identity.png',
        tags: ['logo', 'visual identity', 'style guide']
    },
    {
        titleItalic: 'AI Strategy ',
        titleNormal: 'Consulting',
        subtitle: 'Adopt AI the right way for real business impact.',
        image: '/portfolio/AI Strategy Consulting.png',
        tags: ['automation', 'LLM', 'transformation']
    },
    {
        titleItalic: 'eBook ',
        titleNormal: 'Production',
        subtitle: 'Polished formats for lead magnets and reports.',
        image: '/portfolio/eBook & Digital Reports.png',
        tags: ['content marketing', 'whitepaper', 'PDF']
    },
    {
        titleItalic: 'Concept ',
        titleNormal: 'Creation',
        subtitle: 'Bring rough ideas to life with clarity and creativity.',
        image: '/portfolio/Concept Creation.png',
        tags: ['ideation', 'creative brief', 'branding']
    },
    {
        titleItalic: 'Print ',
        titleNormal: 'Design',
        subtitle: 'Elegant print layouts from brochures to flyers.',
        image: '/portfolio/Print Design.png',
        tags: ['catalogue', 'poster', 'flyer']
    },
    {
        titleItalic: '3D ',
        titleNormal: 'Design',
        subtitle: 'Immersive visuals for interactive and product design.',
        image: '/portfolio/3D & AR Design.png',
        tags: ['modeling', 'augmented reality', 'visualization']
    },
]);

const visibleTagCount = 3;
const splideRef = ref(null);
const activeIndex = ref(0);

// Splide options
const splideOptions = {
    type: 'loop',
    padding: { left: '20px', right: '20px' },
    fixedWidth: 420,
    gap: '20px',
    breakpoints: {
        1280: {
            perPage: 'auto',
            gap: '20px',
            padding: { left: '20px', right: '20px' }
        },
        1024: {
            perPage: 'auto',
            gap: '20px',
            padding: { left: '20px', right: '20px' }
        },
        768: {
            perPage: 'auto',
            gap: '20px',
            padding: { left: '20px', right: '20px' }
        },
        640: {
            perPage: 1,
            gap: '20px',
            padding: { left: '40px', right: '40px' }
        },
    },
    autoplay: true,
    interval: 4000,
    arrows: false,
    pagination: false,
    pauseOnHover: true,
    pauseOnFocus: true,
    keyboard: true,
    drag: true,
    snap: true,
    focus: 'center',
};

// Event handlers
const onSlideMounted = (splide) => {
    activeIndex.value = splide.index;
};

const onSlideMoved = (splide, newIndex) => {
    activeIndex.value = newIndex;
};

const goToSlide = (index) => {
    if (splideRef.value?.splide) {
        splideRef.value.splide.go(index);
    }
};

// Helpers
const isSlideActive = (index) => {
    // For loop type carousel, we need to account for cloned slides
    const totalSlides = cards.value.length;
    const normalizedActiveIndex = activeIndex.value % totalSlides;
    const normalizedIndex = index % totalSlides;
    return normalizedActiveIndex === normalizedIndex;
};

const getVisibleTags = (tags) => tags.slice(0, visibleTagCount);

const handleImageError = (e) => {
    e.target.src = '/placeholder.svg?height=350&width=280';
};

onMounted(() => {
    // Additional setup if needed
});
</script>

<style scoped>
/* Hide default Splide pagination */
.splide__pagination {
    display: none;
}

/* Hide default Splide arrows */
.splide__arrows {
    display: none;
}

/* Ensure proper slide sizing */
.splide__slide {
    display: flex !important;
}

/* Smooth transitions for all interactive elements */
.group {
    will-change: transform;
}
</style>