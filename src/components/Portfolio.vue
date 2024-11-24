<template>
    <!-- Main Content -->
    <main class="container mx-auto px-6 py-12">
        <h1 class="text-4xl font-bold text-center mb-12 text-gray-800">Our Case Studies</h1>

        <div class="flex flex-col lg:flex-row space-y-8 lg:space-y-0 lg:space-x-8">
            <!-- Case Studies List -->
            <div class="lg:w-1/3 bg-gray-100 rounded-xl p-6 shadow-md">
                <div class="flex items-center justify-between mb-6">
                    <h2 class="text-xl font-semibold text-gray-800">Projects</h2>
                    <div class="flex items-center space-x-2">
                        <button class="p-2 hover:bg-gray-200 rounded-lg transition-colors">
                            <Share class="w-4 h-4 text-gray-600" />
                        </button>
                        <button class="p-2 hover:bg-gray-200 rounded-lg transition-colors">
                            <Filter class="w-4 h-4 text-gray-600" />
                        </button>
                    </div>
                </div>

                <div class="space-y-4">
                    <button v-for="filter in filters" :key="filter"
                        class="px-4 py-2 rounded-full text-sm w-full text-left"
                        :class="activeFilter === filter ? 'bg-teal-500 text-white' : 'hover:bg-gray-200 transition-colors text-gray-700'"
                        @click="activeFilter = filter">
                        {{ filter }}
                    </button>
                </div>

                <div class="mt-8 space-y-6">
                    <div v-for="(project, index) in projects" :key="index">
                        <div @click="selectedProject = project"
                            class="p-4 bg-white rounded-lg cursor-pointer hover:bg-gray-50 transition-colors shadow-sm"
                            :class="{ 'border-2 border-teal-500': selectedProject?.id === project.id }">
                            <h3 class="font-medium mb-2 flex items-center justify-between text-gray-800">
                                {{ project.title }}
                                <span :class="`px-2 py-1 rounded-full text-xs ${getPriorityClass(project.priority)}`">
                                    {{ project.priority }}
                                </span>
                            </h3>
                            <div class="flex items-center text-sm text-gray-500 space-x-4">
                                <span class="flex items-center">
                                    <Calendar class="w-4 h-4 mr-1 text-teal-500" />
                                    {{ project.date }}
                                </span>
                                <span class="flex items-center">
                                    <Clock class="w-4 h-4 mr-1 text-teal-500" />
                                    {{ project.duration }}
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Project Details -->
            <div class="lg:w-2/3 bg-gray-100 rounded-xl p-6 shadow-md">
                <div v-if="selectedProject">
                    <div class="flex items-center justify-between mb-6">
                        <h2 class="text-2xl font-bold text-gray-800">{{ selectedProject.title }}</h2>
                        <span :class="`px-3 py-1 rounded-full text-sm ${getPriorityClass(selectedProject.priority)}`">
                            {{ selectedProject.priority }}
                        </span>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
                        <div class="bg-white p-4 rounded-lg shadow-sm">
                            <h3 class="text-lg font-semibold mb-2 text-gray-800">Project Overview</h3>
                            <p class="text-gray-600">{{ selectedProject.description }}</p>
                        </div>
                        <div class="bg-white p-4 rounded-lg shadow-sm">
                            <h3 class="text-lg font-semibold mb-2 text-gray-800">Project Metrics</h3>
                            <div class="space-y-2">
                                <div v-for="(value, key) in selectedProject.metrics" :key="key"
                                    class="flex justify-between">
                                    <span class="text-gray-600">{{ key }}:</span>
                                    <span class="font-medium text-gray-800">{{ value }}</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="mb-8">
                        <h3 class="text-lg font-semibold mb-4 text-gray-800">Project Timeline</h3>
                        <div class="relative">
                            <div class="absolute top-5 left-5 w-[calc(100%-2.5rem)] h-0.5 bg-teal-500"></div>
                            <div class="flex justify-between">
                                <div v-for="(milestone, index) in selectedProject.timeline" :key="index"
                                    class="relative flex flex-col items-center text-center">
                                    <div
                                        class="w-10 h-10 bg-teal-500 rounded-full flex items-center justify-center z-10">
                                        <CheckCircle class="w-6 h-6 text-white" />
                                    </div>
                                    <div class="mt-2 w-24">
                                        <div class="text-xs font-semibold text-gray-800">{{ milestone.event }}</div>
                                        <div class="text-xs text-gray-500">{{ milestone.date }}</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div>
                        <h3 class="text-lg font-semibold mb-4 text-gray-800">Project Gallery</h3>
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                            <img v-for="(image, index) in selectedProject.images" :key="index" :src="image"
                                :alt="`Project image ${index + 1}`"
                                class="w-full h-48 object-cover rounded-lg shadow-sm" />
                        </div>
                    </div>
                </div>
                <div v-else class="flex items-center justify-center h-full text-gray-500">
                    Select a project to view details
                </div>
            </div>
        </div>
    </main>
</template>

<script setup>
import { ref } from 'vue'
import {
    Share, Filter, Calendar, Clock, CheckCircle,
    Twitter, Facebook, Instagram
} from 'lucide-vue-next'

const activeFilter = ref('All Projects')
const selectedProject = ref(null)

const filters = ['All Projects', 'Web Development', 'Mobile Apps', 'UI/UX Design', 'Digital Marketing']

const projects = [
    {
        id: 1,
        title: 'E-commerce Platform Redesign',
        priority: 'High Priority',
        date: 'Jan 15, 2024',
        duration: '3 months',
        description: 'Complete overhaul of a major e-commerce platform, focusing on user experience and conversion rate optimization.',
        metrics: {
            'Conversion Rate': '+25%',
            'Page Load Time': '-40%',
            'Mobile Traffic': '+35%'
        },
        timeline: [
            { event: 'Project Kickoff', date: 'Jan 15, 2024' },
            { event: 'Design Approval', date: 'Feb 1, 2024' },
            { event: 'Development', date: 'Mar 1, 2024' },
            { event: 'Testing', date: 'Apr 1, 2024' },
            { event: 'Launch', date: 'Apr 15, 2024' }
        ],
        images: [
            '/placeholder.svg?height=300&width=400',
            '/placeholder.svg?height=300&width=400',
            '/placeholder.svg?height=300&width=400',
            '/placeholder.svg?height=300&width=400'
        ]
    },
    {
        id: 2,
        title: 'AI-Powered Chatbot Development',
        priority: 'Medium Priority',
        date: 'Mar 1, 2024',
        duration: '2 months',
        description: 'Development of an AI-powered chatbot to enhance customer service efficiency for a global tech company.',
        metrics: {
            'Response Time': '-60%',
            'Customer Satisfaction': '+40%',
            'Query Resolution Rate': '+30%'
        },
        timeline: [
            { event: 'Requirements Gathering', date: 'Mar 1, 2024' },
            { event: 'AI Model Training', date: 'Mar 15, 2024' },
            { event: 'Integration', date: 'Apr 1, 2024' },
            { event: 'Testing', date: 'Apr 15, 2024' },
            { event: 'Deployment', date: 'May 1, 2024' }
        ],
        images: [
            '/placeholder.svg?height=300&width=400',
            '/placeholder.svg?height=300&width=400',
            '/placeholder.svg?height=300&width=400',
            '/placeholder.svg?height=300&width=400'
        ]
    },
    // Add more projects as needed
]

const getPriorityClass = (priority) => {
    const classes = {
        'High Priority': 'bg-orange-500 text-white',
        'Medium Priority': 'bg-yellow-500 text-white',
        'Low Priority': 'bg-green-500 text-white'
    }
    return classes[priority] || 'bg-gray-500 text-white'
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

:root {
    font-family: 'Inter', sans-serif;
}

.bg-teal-500 {
    background-color: #13BBBE;
}

.text-teal-500 {
    color: #13BBBE;
}

.hover\:text-teal-500:hover {
    color: #13BBBE;
}

.bg-orange-500 {
    background-color: #EB4C21;
}

.hover\:bg-orange-600:hover {
    background-color: #D43D15;
}
</style>