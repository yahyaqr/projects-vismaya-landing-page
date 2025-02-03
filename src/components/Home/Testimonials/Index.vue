<template>
    <section class="bg-white px-6 py-8 overflow-hidden">
        <div class="max-w-6xl mx-auto mb-6">
                <span class="text-teal-500 text-sm font-medium tracking-wider uppercase">20+ Happy Clients</span>
                <h2 class="text-2xl font-bold text-gray-900 mt-2">
                    Client Experiences
                </h2>
        </div>

        <div class="max-w-6xl mx-auto space-y-6">
            <ScrollTrack speed="slow" :testimonials="trackOne" />
            <ScrollTrack speed="medium" :testimonials="trackTwo" />
            <ScrollTrack speed="slow" :testimonials="trackThree" />
        </div>
    </section>
</template>

<script setup>
import ScrollTrack from './ScrollTrack.vue'
import { trackOne, trackTwo, trackThree } from './data.js'
</script>
