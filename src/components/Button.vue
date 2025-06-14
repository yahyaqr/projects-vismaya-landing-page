<template>
    <a href="https://wa.me/+628976075402" target="_blank"
        class="flex slide-button items-center gap-2 px-8 py-4 sm:px-10 sm:py-5 rounded-lg bg-white border-2 border-green-500 text-green-500 overflow-hidden relative whatsapp-btn">
        <!-- Default Icon -->
        <img src="/src/assets/whatsapp.svg" class="w-5 h-5 relative z-10 icon-default" />

        <!-- White Icon (for hover) -->
        <img src="/src/assets/whatsapp-white.svg" class="w-5 h-5 relative z-10 icon-hover" />

        <span class="relative z-10">Chat With Us</span>
    </a>
</template>

<style scoped>
.slide-button::before {
    content: '';
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    height: 100%;
    background: #22c55e;
    transition: all 0.3s;
    z-index: 1;
}

.slide-button:hover::before {
    top: 0;
}

.slide-button:hover {
    color: white;
}

.icon-hover {
    display: none;
}

.whatsapp-btn:hover .icon-default {
    display: none;
}

.whatsapp-btn:hover .icon-hover {
    display: inline;
}
</style>