<template>
    <transition name="fade">
        <div v-if="isOpen" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50"
            @keydown.esc="handleKeydown" tabindex="0">
            <!-- Modal Backdrop -->
            <div class="absolute inset-0" @click="closeModal"></div>

            <!-- Modal Content -->
            <div class="bg-white rounded-lg p-8 max-w-md w-full relative z-10" ref="modalContent">
                <h2 class="text-2xl font-bold mb-4 text-gray-800">Placeholder Modal</h2>
                <p class="text-gray-600">This is a blank modal. Click outside to close or press Escape.</p>
                <button @click="closeModal"
                    class="mt-4 px-4 py-2 bg-gray-200 text-gray-800 rounded-lg hover:bg-gray-300 transition-colors">
                    Close
                </button>
            </div>
        </div>
    </transition>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

// Props
defineProps({
    isOpen: Boolean, // Controls the visibility of the modal
    onClose: Function, // Function to handle modal closure
});

// Refs
const modalContent = ref(null);

// Close the modal
const closeModal = () => {
    if (typeof onClose === 'function') {
        onClose();
        console.log("Close modal triggered!");
    }
};

// Handle Escape key to close the modal
const handleKeydown = (event) => {
    if (event.key === 'Escape') {
        closeModal();
    }
};

// Automatically focus on modal content when it opens
onMounted(() => {
    if (modalContent.value) {
        modalContent.value.focus();
    }
});

onUnmounted(() => {
    console.log('Modal unmounted!');
});
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
