<template>
    <div class="relative overflow-hidden bg-black">
        <!-- Background Image -->
        <img src="/src/assets/green-punk.png" class="absolute inset-0 w-full h-full object-cover" />

        <!-- Content Overlay -->
        <div class="relative z-10 flex flex-col min-h-[500px]">
            <!-- Main Content -->
            <div class="flex-grow flex items-center justify-center px-4 sm:px-6 lg:px-8">
                <div class="text-center max-w-4xl mx-auto">
                    <h1 class="text-white text-4xl md:text-6xl font-light leading-tight">
                        Your <span class="italic">creative team's</span>
                        <br />
                        <span class="text-5xl md:text-7xl font-normal">creative team™</span>
                    </h1>

                    <div class="mt-8">
                        <button
                            class="bg-lime-300 hover:bg-lime-400 text-gray-900 font-medium py-3 px-8 rounded-full transition-colors">
                            Book a demo
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { Instagram } from 'lucide-vue-next';
</script>

<style></style>