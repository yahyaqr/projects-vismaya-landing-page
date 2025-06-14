<template>
    <div class="bg-gray-50 p-8 sm:p-16 flex items-center justify-center">
        <div class="w-full max-w-6xl bg-white rounded-2xl shadow-md overflow-hidden">
            <div class="flex flex-col md:flex-row">
                <!-- Image Section -->
                <div class="md:w-1/3 relative h-[200px] md:h-auto">
                    <img src="/src/assets/Foundersy.png" alt="Team collaboration"
                        class="w-full h-full object-cover bg-red" />
                    <!-- <div class="absolute inset-0 bg-gradient-to-r from-black/30 to-transparent"></div> -->
                </div>

                <!-- Content Section -->
                <div class="md:w-2/3 p-6 md:p-8 space-y-6">
                    <div>
                        <span class="text-[#EB4C21] text-sm font-medium tracking-wider uppercase">About us</span>
                        <h2 class="text-2xl font-bold text-gray-900 mt-2">
                            A team built for creativity and technological innovation
                        </h2>
                    </div>

                    <p class="text-gray-600 text-sm leading-relaxed">
                        Vismaya Lab is led by three cofounders and powered by a dynamic team of 4
                        marketing-design professionals and 4 IT specialists. Our Marketing-Design
                        Division excels in enhancing brand visibility and engagement, while our IT
                        Division focuses on cutting-edge software development under Vismaya AI Lab.
                    </p>

                    <!-- Stats Row -->
                    <div class="flex justify-start space-x-12 py-4 border-y border-gray-100">
                        <div class="stat-item">
                            <span class="text-2xl font-bold text-[#EB4C21]">20+</span>
                            <p class="text-xs text-gray-500">Projects delivered</p>
                        </div>
                        <div class="stat-item">
                            <span class="text-2xl font-bold text-[#EB4C21]">90%</span>
                            <p class="text-xs text-gray-500">Client retention</p>
                        </div>
                        <div class="stat-item">
                            <span class="text-2xl font-bold text-[#EB4C21]">11</span>
                            <p class="text-xs text-gray-500">Team members</p>
                        </div>
                    </div>

                    <!-- Etymology -->
                    <div class="text-xs text-gray-500 leading-relaxed bg-gray-50 p-4 rounded-lg">
                        The name "VISMAYA" comes from Sanskrit, meaning 'amazing, remarkable,
                        astonishing.' Derived from the words वि- (vi-, "a part of, something") and स्मय
                        (smaya, "pride, magic, divine illusion"), it reflects our mission to deliver
                        impactful services that elevate our clients' image and drive innovation.
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.stat-item {
    @apply flex flex-col items-start;
}

.stat-item span {
    @apply mb-1;
}
</style>