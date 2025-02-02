<template>
    <section class="container mx-auto px-4 py-8">
        <h2 class="text-3xl font-bold text-center mb-4 text-gray-800 sm:text-4xl">
            Recent Showcase
        </h2>
        <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
            <div v-for="(project, index) in projects" :key="index" class="group relative">
                <img :src="project.image" :alt="project.title"
                    class="w-full h-64 object-cover rounded-lg shadow-lg bg-gray-200" />
                <div class="absolute inset-x-0 bottom-0 p-4 bg-gradient-to-t from-black/40 to-transparent rounded-b-lg">
                    <h3 class="text-lg font-semibold text-white">{{ project.title }}</h3>
                    <p class="text-sm text-gray-300">{{ project.description }}</p>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
const projects = [
    {
        image: '',
        title: 'Web UI Design',
        description: 'Creative UI design.',
    },
    {
        image: '',
        title: 'Digital Strategy',
        description: 'Innovative digital marketing strategy.',
    },
    {
        image: '',
        title: 'UI Design',
        description: 'Sleek and functional UI design.',
    },
];
</script>
