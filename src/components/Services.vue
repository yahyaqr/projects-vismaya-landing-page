<template>
    <div class="bg-gradient-to-br from-gray-50 to-gray-100 py-12 px-4 sm:px-6 lg:px-8">
        <div class="max-w-6xl mx-auto">
            <div class="text-center mb-10">
                <h2 class="text-3xl sm:text-4xl font-bold text-center mb-12 text-gray-800">
                    High-impact services<br />
                    for your business
                </h2>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div v-for="service in services" :key="service.title"
                    class="group relative bg-white rounded-xl overflow-hidden transition-all duration-300 hover:shadow-xl"
                    :class="{ 'ring-2 ring-teal-500 ring-offset-2': service.popular }">
                    <!-- Popular Badge -->
                    <div v-if="service.popular"
                        class="absolute top-2 right-2 bg-teal-500 text-white text-xs font-medium px-2 py-0.5 rounded-full">
                        Popular
                    </div>

                    <div class="p-5">
                        <!-- Icon with animated background -->
                        <div class="relative inline-flex items-center justify-center w-12 h-12 rounded-xl mb-4 
                       bg-gradient-to-br from-teal-50 to-teal-100 group-hover:from-teal-100 group-hover:to-teal-200 
                       transition-all duration-300">
                            <component :is="service.icon"
                                class="w-6 h-6 text-teal-600 transform group-hover:scale-110 transition-transform duration-300" />
                            <div
                                class="absolute inset-0 rounded-xl bg-teal-500 opacity-0 group-hover:opacity-10 transition-opacity duration-300">
                            </div>
                        </div>

                        <!-- Content -->
                        <h3
                            class="text-xl font-bold text-gray-900 mb-2 group-hover:text-teal-600 transition-colors duration-300">
                            {{ service.title }}
                        </h3>

                        <p class="text-sm text-gray-600 mb-4 h-12 leading-snug line-clamp-2">
                            {{ service.description }}
                        </p>

                        <!-- Features List -->
                        <ul class="space-y-1 mb-4">
                            <li v-for="feature in service.features" :key="feature"
                                class="flex items-center text-gray-600">
                                <CheckIcon class="w-4 h-4 text-teal-500 mr-1 flex-shrink-0" />
                                <span class="text-xs">{{ feature }}</span>
                            </li>
                        </ul>

                        <!-- Price -->
                        <div class="mb-4 text-sm">
                            <span class="text-gray-500">Starting from</span>
                            <div class="font-bold text-gray-900">
                                {{ service.price.split(' - ')[0] }}
                                <span class="text-xs font-normal text-gray-500"> - {{ service.price.split(' - ')[1]
                                    }}</span>
                            </div>
                        </div>

                        <!-- Action Button -->
                        <!-- <button class="w-full py-2 px-4 rounded-lg text-sm font-semibold transition-all duration-300
                       bg-gradient-to-r from-teal-500 to-teal-600 hover:from-teal-600 hover:to-teal-700
                       text-white shadow-md shadow-teal-500/20 hover:shadow-teal-500/30
                       transform hover:-translate-y-0.5 active:translate-y-0">
                            <div class="flex items-center justify-center space-x-1">
                                <span>See Package</span>
                                <ArrowRightIcon
                                    class="w-4 h-4 transition-transform duration-300 group-hover:translate-x-0.5" />
                            </div>
                        </button> -->
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import {
    PenLine,
    Layout,
    BarChart2,
    Globe,
    Settings,
    Briefcase,
    Check as CheckIcon,
    ArrowRight as ArrowRightIcon
} from 'lucide-vue-next'

const services = [
    {
        icon: PenLine,
        title: 'Content Marketing',
        description: 'We create engaging content to boost your brand awareness and drive engagement.',
        price: 'IDR 500,000 - IDR 1,500,000',
        popular: true,
        features: [
            'Social media content',
            'Blog articles',
            'Email newsletters',
            'Content strategy'
        ]
    },
    {
        icon: Layout,
        title: 'Graphic Design',
        description: 'Creative graphic design services to make your brand stand out.',
        price: 'IDR 300,000 - IDR 1,000,000',
        features: [
            'Logo design',
            'Brand guidelines',
            'Marketing materials',
            'Social media graphics'
        ]
    },
    {
        icon: BarChart2,
        title: 'Digital Marketing',
        description: 'Reach your target audience with effective digital marketing strategies.',
        price: 'IDR 800,000 - IDR 2,500,000',
        popular: true,
        features: [
            'SEO optimization',
            'PPC campaigns',
            'Social media marketing',
            'Analytics & reporting'
        ]
    },
    {
        icon: Globe,
        title: 'Web Design',
        description: 'Beautiful and functional websites designed to deliver results.',
        price: 'IDR 1,200,000 - IDR 5,000,000',
        features: [
            'Responsive design',
            'UX optimization',
            'Performance tuning',
            'SEO friendly'
        ]
    },
    {
        icon: Settings,
        title: 'IT Consulting',
        description: 'Expert guidance on technology solutions tailored to your business needs.',
        price: 'IDR 1,000,000 - IDR 3,000,000',
        features: [
            'Technical assessment',
            'Solution architecture',
            'Security audit',
            'Cloud consulting'
        ]
    },
    {
        icon: Briefcase,
        title: 'Brand Identity',
        description: 'We help establish and grow your brand identity across all channels.',
        price: 'IDR 600,000 - IDR 2,000,000',
        features: [
            'Brand strategy',
            'Visual identity',
            'Brand guidelines',
            'Voice & tone'
        ]
    }
]
</script>