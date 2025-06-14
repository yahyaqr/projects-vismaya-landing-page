<template>
    <div class="text-gray-800 font-sans select-none">
        <div
            class="flex flex-col justify-center items-center gap-4 lg:gap-8 h-[400px] sm:h-[600px] lg:h-[800px] bg-[#000000] overflow-hidden">
            <Hero />
        </div>

        <div class=" lg:h-[800px] sm:h-[600px] h-[400px] flex flex-col justify-center items-center gap-8 lg:gap-8
        bg-[#1A1A1A] bg-texture ">
            <Message />
        </div>

        <div class="flex flex-col justify-center items-center gap-4 lg:gap-8 sm:min-h-[80vh] bg-white">
            <Entrepreneurs />
        </div>

        <hr class="h-px my-1 mx-8 bg-gray-400 border-0 dark:bg-gray-700" />

        <div class="flex flex-col justify-center items-center gap-4 lg:gap-8 sm:min-h-[80vh] bg-white">
            <FreelancerTrouble />
        </div>

        <hr class="h-px my-1 mx-8 bg-gray-400 border-0 dark:bg-gray-700" />

        <div class="flex flex-col justify-center items-center gap-4 lg:gap-8 sm:min-h-[80vh] bg-white">
            <RealNeeds />
        </div>

        <hr class="h-px my-1 mx-8 bg-gray-400 border-0 dark:bg-gray-700" />

        <div class="flex flex-col justify-center items-center gap-4 lg:gap-8 sm:min-h-[80vh] bg-white">
            <VismayaPositioning />
        </div>

        <!-- <hr class="h-px my-1 mx-8 bg-gray-400 border-0 dark:bg-gray-700" /> -->

        <!-- <div class="flex flex-col justify-center items-center gap-4 lg:gap-8 sm:min-h-[80vh] bg-white">
            <WhyVismaya />
        </div> -->

        <!-- <div class="flex flex-col justify-center items-center gap-4 lg:gap-8 sm:min-h-[80vh] bg-[#1A1A1A]">
            <Chat />
        </div> -->

        <div
            class="flex flex-col justify-center items-center gap-4 lg:gap-8 sm:min-h-[80vh] bg-[#1A1A1A]  overflow-hidden bg-texture">
            <PreviousWorks />
        </div>

        <div
            class="flex flex-col justify-center items-center gap-4 lg:gap-8 sm:min-h-[80vh] bg-[#000000] overflow-hidden">
            <Clients />
        </div>

        <Statement />

        <!-- <div class="lg:h-[800px] sm:h-[600px] h-[400px] flex flex-col justify-center items-center gap-8 bg-[#F8F9F3]">
            <div class="h-full w-full">
                <SocialProof />
            </div>
        </div> -->

        <!-- <div class="lg:h-[800px] sm:h-[600px] h-[400px] flex flex-col justify-center items-center gap-4 lg:gap-8">
            <AddressingObjections />
        </div> -->

        <!-- <div class="lg:h-[800px] sm:h-[600px] h-[400px] flex flex-col justify-center items-center gap-8 bg-[#F8F9F3]">
            <div class="h-full w-full">
                <ClientsWeHaveWorkedOn />
            </div>
        </div> -->

        <!-- <Clients /> -->

        <!-- <Services /> -->

        <!-- <About /> -->

        <!-- <Showcase /> -->

        <!-- <Testimonials /> -->

        <!-- <CTA /> -->

        <Footer />
    </div>
</template>

<script setup>
// Importing the modularized components
import Hero from '../components/Home/Hero.vue';
import Message from '../components/Home/Message.vue';
import Entrepreneurs from '../components/Home/Entrepreneurs.vue';
import FreelancerTrouble from '../components/Home/FreelancerTrouble.vue';
import RealNeeds from '../components/Home/RealNeeds.vue';
import VismayaPositioning from '../components/Home/VismayaPositioning.vue';
// import WhyVismaya from '../components/Home/WhyVismaya.vue';
// import Chat from '../components/Home/Chat.vue';
import PreviousWorks from '../components/Home/PreviousWorks.vue';
import Clients from '../components/Home/Clients.vue';
import Statement from '../components/Home/Statement.vue';
// import SocialProof from '../components/Home/SocialProof.vue';
// import AddressingObjections from '../components/Home/AddressingObjections.vue';
// import ClientsWeHaveWorkedOn from '../components/Home/ClientsWeHaveWorkedOn.vue';
// import Clients from '../components/Home/Clients.vue';
// import Services from '../components/Home/Services/Index.vue';
// import About from '../components/Home/About.vue';
// import Testimonials from '../components/Home/Testimonials/Index.vue';
// import Showcase from '../components/Home/Showcase.vue';
// import CTA from '../components/Home/CTA.vue';
import Footer from '../components/Footer.vue';
</script>

<style>
.bg-texture {
    background-image: url('/src/assets/texture.png');
    background-repeat: repeat;
    background-size: auto;
}
</style>