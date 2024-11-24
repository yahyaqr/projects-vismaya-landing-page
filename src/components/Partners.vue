<template>
    <section class="container mx-auto px-4 py-12 border-t border-gray-200">
        <p class="text-center text-sm text-gray-500 mb-8">Trusted by Leading Brands</p>
        <div class="flex flex-wrap justify-center gap-8 opacity-70">
            <div v-for="i in 6" :key="i" class="w-24 h-12 bg-gray-200 rounded"></div>
        </div>
    </section>
</template>