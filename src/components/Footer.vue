<template>
    <footer class="container mx-auto px-4 flex justify-between items-center bg-white py-4 border-t border-gray-200">
        <div class="mb-6 md:mb-0">
            <div class="text-4xl mb-2 flex flex-wrap gap-1 items-end">
                <span class="font-playfair font-bold">Vismaya</span>
            </div>
        </div>
        <div class="flex flex-wrap justify-center gap-6 mb-6 md:mb-0 font-sans">
            <a href="#" class="text-gray-500 hover:text-black transition-colors">Privacy policy</a>
            <a href="#" class="text-gray-500 hover:text-black transition-colors">Terms of use</a>
            <a href="#" class="text-gray-500 hover:text-black transition-colors">Status page</a>
            <a href="#" class="text-gray-500 hover:text-black transition-colors">DMCA</a>
        </div>
        <div class="flex gap-4">
            <a href="https://www.instagram.com/vismaya.id/" target="_blank"
                class="text-gray-500 hover:text-black p-2 border border-black/20 hover:border-black rounded-full transition-colors">
                <Instagram class="w-5 h-5" />
            </a>
            <a href="https://www.instagram.com/more.activ/" target="_blank"
                class="text-gray-500 hover:text-black p-2 border border-black/20 hover:border-black rounded-full transition-colors">
                <Instagram class="w-5 h-5" />
            </a>
        </div>
    </footer>
</template>

<script setup>
import { Instagram } from 'lucide-vue-next';
</script>

<style scoped>
.font-playfair {
    font-family: 'Playfair Display', serif;
    letter-spacing: -0.02em;
}
</style>