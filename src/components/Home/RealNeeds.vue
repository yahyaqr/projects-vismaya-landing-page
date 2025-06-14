<template>
    <section class="w-full text-black py-16 px-4 sm:py-20 sm:px-6 md:px-8 font-inter">
        <div class="max-w-7xl mx-auto space-y-12">
            <h1
                class="text-3xl sm:text-4xl md:text-5xl font-extrabold tracking-tight leading-tight text-center font-playfair">
                What they really need is…
            </h1>

            <div class="flex flex-col gap-8 sm:gap-10 mx-auto">
                <div class="bg-gray-50 border-l-4 border-black p-5 sm:p-6 rounded-sm">
                    <h2 class="text-2xl sm:text-3xl font-playfair-2 font-bold flex items-center mb-3 sm:mb-4">
                        <BrainIcon class="mr-3 h-7 w-7 sm:h-8 sm:w-8" />
                        Strategy
                    </h2>
                </div>

                <div class="bg-gray-50 border-l-4 border-black p-5 sm:p-6 rounded-sm">
                    <h2 class="text-2xl sm:text-3xl font-playfair-2 font-bold flex items-center mb-3 sm:mb-4">
                        <PaletteIcon class="mr-3 h-7 w-7 sm:h-8 sm:w-8" />
                        Brand & Design
                    </h2>
                </div>

                <div class="bg-gray-50 border-l-4 border-black p-5 sm:p-6 rounded-sm">
                    <h2 class="text-2xl sm:text-3xl font-playfair-2 font-bold flex items-center mb-3 sm:mb-4">
                        <TrendingUpIcon class="mr-3 h-7 w-7 sm:h-8 sm:w-8" />
                        Marketing
                    </h2>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { BrainIcon, PaletteIcon, HammerIcon, TrendingUpIcon, ArrowRightIcon } from 'lucide-vue-next';
</script>

<style scoped></style>
