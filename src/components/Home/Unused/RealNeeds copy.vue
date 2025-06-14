<template>
    <section class="w-full text-black py-16 px-4 sm:py-20 sm:px-6 md:px-8 font-inter">
        <div class="max-w-7xl mx-auto space-y-12">
            <h1
                class="text-3xl sm:text-4xl md:text-5xl font-extrabold tracking-tight leading-tight text-center font-playfair">
                What they really need is…
            </h1>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 sm:gap-10 mx-auto">
                <div class="bg-gray-50 border-l-4 border-black p-5 sm:p-6 rounded-sm">
                    <h2 class="text-2xl sm:text-3xl font-playfair-2 font-bold flex items-center mb-3 sm:mb-4">
                        <BrainIcon class="mr-3 h-7 w-7 sm:h-8 sm:w-8" />
                        Strategy
                    </h2>
                    <ul class="space-y-2 sm:space-y-3 font-mono">
                        <li class="flex items-start text-base sm:text-xl">
                            <ArrowRightIcon class="h-5 w-5 mr-2 mt-0.5 flex-shrink-0" />
                            <span>"Is this a real opportunity?"</span>
                        </li>
                        <li class="flex items-start text-base sm:text-xl">
                            <ArrowRightIcon class="h-5 w-5 mr-2 mt-0.5 flex-shrink-0" />
                            <span>"What's the clearest angle?"</span>
                        </li>
                    </ul>
                </div>

                <div class="bg-gray-50 border-l-4 border-black p-5 sm:p-6 rounded-sm">
                    <h2 class="text-2xl sm:text-3xl font-playfair-2 font-bold flex items-center mb-3 sm:mb-4">
                        <PaletteIcon class="mr-3 h-7 w-7 sm:h-8 sm:w-8" />
                        Brand & Design
                    </h2>
                    <ul class="space-y-2 sm:space-y-3 font-mono">
                        <li class="flex items-start text-base sm:text-xl">
                            <ArrowRightIcon class="h-5 w-5 mr-2 mt-0.5 flex-shrink-0" />
                            <span>"Why doesn't it feel professional yet?"</span>
                        </li>
                        <li class="flex items-start text-base sm:text-xl">
                            <ArrowRightIcon class="h-5 w-5 mr-2 mt-0.5 flex-shrink-0" />
                            <span>"What colors? Fonts? Voice?"</span>
                        </li>
                    </ul>
                </div>

                <div class="bg-gray-50 border-l-4 border-black p-5 sm:p-6 rounded-sm">
                    <h2 class="text-2xl sm:text-3xl font-playfair-2 font-bold flex items-center mb-3 sm:mb-4">
                        <HammerIcon class="mr-3 h-7 w-7 sm:h-8 sm:w-8" />
                        Execution
                    </h2>
                    <ul class="space-y-2 sm:space-y-3 font-mono">
                        <li class="flex items-start text-base sm:text-xl">
                            <ArrowRightIcon class="h-5 w-5 mr-2 mt-0.5 flex-shrink-0" />
                            <span>"I need a deck. A site. A plan. Some posts."</span>
                        </li>
                        <li class="flex items-start text-base sm:text-xl">
                            <ArrowRightIcon class="h-5 w-5 mr-2 mt-0.5 flex-shrink-0" />
                            <span>"Can you just… help me launch this?"</span>
                        </li>
                    </ul>
                </div>

                <div class="bg-gray-50 border-l-4 border-black p-5 sm:p-6 rounded-sm">
                    <h2 class="text-2xl sm:text-3xl font-playfair-2 font-bold flex items-center mb-3 sm:mb-4">
                        <TrendingUpIcon class="mr-3 h-7 w-7 sm:h-8 sm:w-8" />
                        Marketing
                    </h2>
                    <ul class="space-y-2 sm:space-y-3 font-mono">
                        <li class="flex items-start text-base sm:text-xl">
                            <ArrowRightIcon class="h-5 w-5 mr-2 mt-0.5 flex-shrink-0" />
                            <span>"Cool idea. But how do I get leads?"</span>
                        </li>
                        <li class="flex items-start text-base sm:text-xl">
                            <ArrowRightIcon class="h-5 w-5 mr-2 mt-0.5 flex-shrink-0" />
                            <span>"How do I scale this?"</span>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { BrainIcon, PaletteIcon, HammerIcon, TrendingUpIcon, ArrowRightIcon } from 'lucide-vue-next';
</script>

<style scoped></style>
