<template>
    <section class="container mx-auto px-4 py-20">
        <h2 class="text-3xl sm:text-4xl font-bold text-center mb-12 text-gray-800">
            High-impact services<br />
            for your business
        </h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
            <!-- Cards -->
            <div v-for="(service, index) in services" :key="index"
                class="bg-white p-6 rounded-lg shadow-lg hover:shadow-xl transition-shadow">
                <!-- Icon -->
                <div class="w-12 h-12 rounded-full bg-teal-100 flex items-center justify-center mb-4">
                    <component :is="service.icon" class="w-6 h-6 text-teal-500" />
                </div>
                <!-- Title -->
                <h3 class="text-xl font-semibold mb-2 text-gray-800">{{ service.title }}</h3>
                <!-- Description -->
                <p class="text-gray-600 mb-4">{{ service.description }}</p>
                <!-- Price Range -->
                <p class="text-teal-500 text-sm font-semibold mb-2">Starting from: {{ service.priceRange }}</p>
                <!-- See Package Button -->
                <button @click="openPackageModal(index)"
                    class="w-full bg-gray-100 text-gray-800 font-medium py-2 rounded-lg hover:bg-gray-200 transition-colors">
                    See Package
                </button>
            </div>
        </div>

        <!-- Modal -->
        <div v-if="activeService !== null"
            class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4"
            @click.self="closePackageModal">
            <div class="bg-white rounded-lg px-4 py-5 sm:px-6 sm:py-6 max-w-3xl w-full relative shadow-lg">
                <!-- Modal Title -->
                <h2 class="text-lg font-bold text-teal-500 mb-6 text-center">
                    {{ services[activeService].title }} - Packages and Prices
                </h2>
                <!-- Horizontal Packages -->
                <div class="flex flex-wrap gap-4 justify-center">
                    <div v-for="(packageInfo, idx) in services[activeService].packages" :key="idx"
                        class="border border-gray-300 rounded-lg p-4 w-full xs:w-[90%] sm:w-[48%] lg:w-[30%] min-w-[280px] flex flex-col">
                        <div class="flex justify-between items-center mb-2">
                            <h3 class="text-sm font-semibold text-teal-500">{{ packageInfo.name }}</h3>
                            <span class="text-teal-500 font-semibold">{{ packageInfo.price }}</span>
                        </div>
                        <p class="text-sm text-gray-600 mb-2">
                            <i class="far fa-calendar"></i> Duration: {{ packageInfo.duration }}
                        </p>
                        <p class="text-sm text-gray-700 whitespace-pre-line">{{ packageInfo.description }}</p>
                    </div>
                </div>
            </div>
        </div>


    </section>
</template>

<script setup>
import { ref } from "vue";
import { Pencil, Layout, BarChart, PenTool, BrainCircuit } from "lucide-vue-next";

const services = ref([
    {
        icon: Pencil,
        title: "Content Marketing",
        description: "We create engaging content to boost your brand awareness and drive engagement.",
        priceRange: "IDR 500,000 - IDR 1,500,000",
        packages: [
            {
                name: "Basic Content Package",
                price: "IDR 500,000",
                duration: "2 Days",
                description: "- 3 Blog Articles\n- Basic Copywriting\n- Free Consultation",
            },
            {
                name: "Standard Content Package",
                price: "IDR 1,000,000",
                duration: "4 Days",
                description: "- 5 Blog Articles\n- Advanced Copywriting\n- Content Planning\n- Free Consultation",
            },
            {
                name: "Premium Content Package",
                price: "IDR 1,500,000",
                duration: "7 Days",
                description: "- 10 Blog Articles\n- Advanced Copywriting\n- SEO Optimization\n- Free Consultation and Final Report",
            },
        ],
    },
    {
        icon: Layout,
        title: "Graphic Design",
        description: "Creative graphic design services to make your brand stand out.",
        priceRange: "IDR 300,000 - IDR 1,000,000",
        packages: [
            {
                name: "Basic Design Package",
                price: "IDR 300,000",
                duration: "3 Days",
                description: "- 3 Feed Posts\n- 1 Story Design\n- 2 Free Revisions",
            },
            {
                name: "Standard Design Package",
                price: "IDR 600,000",
                duration: "5 Days",
                description: "- 5 Feed Posts\n- 3 Story Designs\n- High-Resolution Files\n- 3 Free Revisions",
            },
            {
                name: "Premium Design Package",
                price: "IDR 1,000,000",
                duration: "7 Days",
                description: "- 10 Feed Posts\n- 5 Story Designs\n- Unlimited Revisions\n- Branding Guide and Master Files",
            },
        ],
    },
    {
        icon: BarChart,
        title: "Digital Marketing",
        description: "Reach your target audience with effective digital marketing strategies.",
        priceRange: "IDR 800,000 - IDR 2,500,000",
        packages: [
            {
                name: "Basic Marketing Package",
                price: "IDR 800,000",
                duration: "5 Days",
                description: "- Social Media Campaign\n- 3 Sponsored Posts\n- Basic Analytics",
            },
            {
                name: "Advanced Marketing Package",
                price: "IDR 1,500,000",
                duration: "10 Days",
                description: "- Social Media Campaign\n- 5 Sponsored Posts\n- Advanced Analytics and Optimization",
            },
            {
                name: "Enterprise Marketing Package",
                price: "IDR 2,500,000",
                duration: "14 Days",
                description: "- Full Campaign Management\n- Custom Ad Designs\n- A/B Testing and Optimization\n- Comprehensive Analytics Report",
            },
        ],
    },
    {
        icon: PenTool,
        title: "Web Design",
        description: "Beautiful and functional websites designed to deliver results.",
        priceRange: "IDR 1,200,000 - IDR 5,000,000",
        packages: [
            {
                name: "Starter Website Package",
                price: "IDR 1,200,000",
                duration: "7 Days",
                description: "- 3 Pages (Home, About, Contact)\n- Mobile Responsive\n- Basic SEO",
            },
            {
                name: "Business Website Package",
                price: "IDR 3,000,000",
                duration: "14 Days",
                description: "- 5 Pages (Home, Services, About, Contact, Blog)\n- Mobile Responsive\n- SEO Optimized\n- CMS Integration",
            },
            {
                name: "Premium Website Package",
                price: "IDR 5,000,000",
                duration: "21 Days",
                description: "- Custom Design\n- Unlimited Pages\n- E-commerce Integration\n- Advanced SEO and 1-Month Maintenance",
            },
        ],
    },
    {
        icon: BrainCircuit,
        title: "IT Consulting",
        description: "Expert guidance on technology solutions tailored to your business needs.",
        priceRange: "IDR 1,000,000 - IDR 3,000,000",
        packages: [
            {
                name: "Basic Consulting Package",
                price: "IDR 1,000,000",
                duration: "2 Days",
                description: "- IT Needs Analysis\n- Basic IT Solutions Report\n- 1 Free Consultation",
            },
            {
                name: "Advanced Consulting Package",
                price: "IDR 2,000,000",
                duration: "5 Days",
                description: "- Comprehensive IT Needs Analysis\n- Latest Technology Recommendations\n- 3 Free Consultations",
            },
            {
                name: "Custom Consulting Package",
                price: "IDR 3,000,000",
                duration: "7 Days",
                description: "- Customized IT Solutions\n- Basic Implementation\n- Unlimited Free Consultations",
            },
        ],
    },
    {
        icon: BarChart,
        title: "Brand Identity",
        description: "We help establish and grow your brand identity across all channels.",
        priceRange: "IDR 600,000 - IDR 2,000,000",
        packages: [
            {
                name: "Starter Branding Package",
                price: "IDR 600,000",
                duration: "3 Days",
                description: "- Logo Design\n- Color Palette and Typography\n- Basic Branding Guidelines",
            },
            {
                name: "Professional Branding Package",
                price: "IDR 1,200,000",
                duration: "7 Days",
                description: "- Logo Design\n- Full Branding Kit (Color Palette, Typography, Iconography)\n- Social Media Templates\n- Advanced Branding Guidelines",
            },
            {
                name: "Complete Branding Package",
                price: "IDR 2,000,000",
                duration: "10 Days",
                description: "- Custom Logo and Visual Identity Design\n- Full Branding Kit\n- Marketing Materials Design (Brochures, Posters, etc.)\n- Comprehensive Branding Guidelines",
            },
        ],
    },
]);

const activeService = ref(null);

// Open modal for a specific service
const openPackageModal = (index) => {
    activeService.value = index;
};

// Close the modal
const closePackageModal = () => {
    activeService.value = null;
};
</script>