<template>
    <section class="bg-gray-50 py-16 px-4 sm:px-6 lg:px-8">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-end mb-12">
                <div class="max-w-2xl">
                    <span class="text-teal-500 text-sm font-medium tracking-wider uppercase">Our Work</span>
                    <h2 class="text-2xl font-bold text-gray-900 mt-2">
                        Transforming ideas into digital experiences that inspire
                    </h2>
                </div>

                <!-- <a href="#"
                    class="inline-flex items-center text-sm font-medium text-teal-600 hover:text-teal-700 transition-colors duration-200">
                    View all portfolio
                    <ArrowRightIcon class="w-4 h-4 ml-1" />
                </a> -->
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <article v-for="(item, index) in showcaseItems" :key="index"
                    class="group relative overflow-hidden rounded-2xl shadow-lg transition-transform duration-300 hover:-translate-y-2">
                    <div class="aspect-w-16 aspect-h-9 w-full">
                        <div :src="item.image" :alt="item.title"
                            class="h-full w-full object-cover transition-transform duration-500 group-hover:scale-105"
                            @error="handleImageError($event, index)" />
                    </div>

                    <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/40 to-transparent">
                        <div class="absolute bottom-0 p-6">
                            <h3 class="text-2xl font-bold text-white mb-2">
                                {{ item.title }}
                            </h3>
                            <p class="text-gray-200 text-sm">
                                {{ item.description }}
                            </p>
                        </div>
                    </div>

                    <div
                        class="absolute inset-0 bg-black/60 opacity-0 transition-opacity duration-300 group-hover:opacity-100">
                        <div class="flex h-full items-center justify-center">
                            <button
                                class="rounded-full bg-white px-6 py-2 text-sm font-semibold text-black transition-transform duration-300 hover:bg-gray-100">
                                View Project
                            </button>
                        </div>
                    </div>
                </article>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue'
import { ArrowRightIcon } from 'lucide-vue-next'

const showcaseItems = ref([
    {
        title: 'E-Commerce Revolution',
        description: 'Reimagining online shopping with AI-powered personalization.',
        image: ''
    },
    {
        title: 'HealthTech Platform',
        description: 'Connecting patients and healthcare providers seamlessly.',
        image: ''
    },
    {
        title: 'Smart City Dashboard',
        description: 'Visualizing urban data for better city management.',
        image: ''
    }
])

const handleImageError = (event, index) => {
    event.target.src = `/placeholder.svg?height=400&width=600`
}
</script>

<style scoped>
.aspect-w-16 {
    position: relative;
    padding-bottom: 56.25%;
}

.aspect-w-16>* {
    position: absolute;
    height: 100%;
    width: 100%;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
}
</style>