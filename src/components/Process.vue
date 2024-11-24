<template>
    <section class="container mx-auto px-4 py-20">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
            <!-- Left Column: Rotating Circular Process -->
            <div class="relative w-[400px] h-[400px] mx-auto">
                <!-- Background Circle -->
                <div class="absolute inset-0 rounded-full border-2 border-dashed border-gray-300 animate-spin-slow">
                </div>

                <!-- Circular steps -->
                <div v-for="(step, index) in process" :key="index" :style="getPositionStyle(index, process.length)"
                    class="absolute flex flex-col items-center justify-center bg-white p-6 rounded-lg shadow-lg w-40 h-30 text-center">
                    <component :is="step.icon" class="w-8 h-8 mb-2 text-teal-500" />
                    <h3 class=" font-semibold text-gray-800">
                        {{ step.title }}
                    </h3>
                </div>
            </div>

            <!-- Right Column: Summary -->
            <div>
                <h3 class=" text-teal-500 mb-4">Our Process</h3>
                <h2 class="text-3xl sm:text-4xl font-bold text-gray-800 mb-6">
                    Measurable Growth, Sustainable Success
                </h2>
                <p class=" sm:text-base text-gray-600 mb-4">
                    At Vismaya, we leverage the Entrepreneurial Operating System (EOS) to align goals, streamline
                    operations, and track key metrics.
                </p>
                <ul class="list-disc list-inside sm:text-base text-gray-600 space-y-2">
                    <li><strong>Vision:</strong> Clear goals for growth.</li>
                    <li><strong>Data:</strong> Weekly tracking for insights.</li>
                    <li><strong>Process:</strong> Efficient workflows.</li>
                    <li><strong>People:</strong> Right roles, done right.</li>
                    <li><strong>Issues:</strong> Identify and resolve roadblocks.</li>
                </ul>
                <p class="sm:text-base text-gray-600 mt-4">
                    From social media activation to ads and content strategies, Vismaya ensures scalable, impactful
                    digital solutions.
                </p>
            </div>
        </div>
    </section>
</template>

<script setup>
import { Map, BarChart, Settings, Users, AlertTriangle } from "lucide-vue-next";

const process = [
    {
        icon: BarChart,
        title: "2. Data",
    },
    {
        icon: Settings,
        title: "3. Process",
    },
    {
        icon: Users,
        title: "4. People",
    },
    {
        icon: AlertTriangle,
        title: "5. Issues",
    },
    {
        icon: Map,
        title: "1. Vision",
    },
];

const getPositionStyle = (index, total) => {
    const angle = (360 / total) * index; // Calculate angle for each item
    const radius = 150; // Circle radius
    const x = radius * Math.cos((angle * Math.PI) / 180); // X coordinate
    const y = radius * Math.sin((angle * Math.PI) / 180); // Y coordinate
    return {
        transform: `translate(-50%, -50%) translate(${x}px, ${y}px)`,
        top: "50%",
        left: "50%",
    };
};
</script>

<style scoped>
/* Animation for spinning */
@keyframes spin-slow {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}

.animate-spin-slow {
    animation: spin-slow 10s linear infinite;
}
</style>
