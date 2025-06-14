<template>
    <section
        class="relative w-full min-h-screen px-4 sm:px-8 lg:px-16 xl:px-32 flex justify-center items-center text-center text-white overflow-hidden font-sans">

        <!-- Text Content -->
        <div class="w-full py-16 sm:py-24 lg:py-32 z-10 relative">
            <h1
                class="text-5xl sm:text-6xl md:text-7xl lg:text-8xl font-extrabold leading-tight uppercase mb-4 sm:mb-6 bg-gradient-to-r from-white/100 to-[#9C9C9C] text-transparent bg-clip-text">
                Stop planning<br class="inline" />
                start
                <span class="inline-block">
                    {{ displayText }}
                    <span v-if="showCursor" class="cursor-line"></span>
                </span>
            </h1>
            <p
                class="text-gray-300 text-xl sm:text-3xl xl:text-4xl leading-relaxed bg-gradient-to-r from-white/100 to-[#9C9C9C] text-transparent bg-clip-text">
                Plans are good. Execution is 1000x better.
            </p>
        </div>

        <!-- Background Logo -->
        <div class="absolute bottom-0 right-0 w-[50%] translate-x-[10%] translate-y-[10%] opacity-5 z-0">
            <img src="/src/assets/vismaya-logo.png" alt="Vismaya Logo" class="w-full h-auto" />
        </div>
    </section>
</template>

<script setup>
import { ref } from "vue";

const original = "doing";
const target = "earning";
const displayText = ref(original);
const showCursor = ref(false);

setTimeout(() => {
    showCursor.value = true;

    setTimeout(() => {
        let i = original.length;
        const deleteInterval = setInterval(() => {
            displayText.value = displayText.value.slice(0, --i);
            if (i === 0) {
                clearInterval(deleteInterval);

                setTimeout(() => {
                    let j = 0;
                    const typeInterval = setInterval(() => {
                        displayText.value += target[j++];
                        if (j === target.length) {
                            clearInterval(typeInterval);
                            showCursor.value = false;
                        }
                    }, 50);
                }, 1000); // delay before typing starts
            }
        }, 50);
    }, 1000); // delay after cursor appears, before deleting starts
}, 2000);
</script>

<style scoped>
.cursor-line {
    margin-bottom: -10px;
    display: inline-block;
    width: 2px;
    height: 90px;
    background-color: white;
    animation: blink 1s step-end infinite;
}

@keyframes blink {

    0%,
    100% {
        opacity: 1;
    }

    50% {
        opacity: 0;
    }
}
</style>
