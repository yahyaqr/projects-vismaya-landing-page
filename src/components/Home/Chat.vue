<template>
    <div class="relative lg:h-screen w-full overflow-hidden flex flex-col justify-center items-center">
        <!-- Left content (sticky) -->
        <div
            class="lg:absolute w-full inset-0 flex flex-col justify-start lg:justify-center px-6 lg:px-20 py-12 md:pt-24 z-0">
            <!-- Navigation Arrows - Positioned above the content -->
            <div class="absolute top-10 left-10 items-center gap-4 hidden lg:flex">
                <button @click="prev" class="carousel-arrow">
                    <ChevronLeft class="w-5 h-5" />
                </button>
                <button @click="next" class="carousel-arrow">
                    <ChevronRight class="w-5 h-5" />
                </button>
            </div>

            <div class="space-y-6">
                <!-- Static content - no animation -->
                <h2 class="text-xs sm:text-sm font-mono text-gray-400 tracking-widest uppercase">
                    Turning Plans Into Execution
                </h2>

                <!-- Dynamic content with animations -->
                <div class="dynamic-content max-w-xl">
                    <p class="text-2xl sm:text-3xl text-white font-playfair leading-tight transition-all duration-500"
                        :class="{ 'opacity-0 translate-y-4': isTransitioning, 'opacity-100 translate-y-0': !isTransitioning }">
                        Step {{ activeSection + 1 }} of {{ sectionInfo.length }}<br />
                        <span class="text-3xl sm:text-5xl italic font-bold">{{ sectionInfo[activeSection].title
                            }}</span>
                    </p>
                    <p class="text-lg text-gray-300 font-sans leading-relaxed mt-6 transition-all duration-500 delay-100"
                        :class="{ 'opacity-0 translate-y-4': isTransitioning, 'opacity-100 translate-y-0': !isTransitioning }">
                        At this stage, we help founders with <span class="font-semibold text-white lowercase">{{
                    sectionInfo[activeSection].title }}</span> —
                        <span>{{ sectionInfo[activeSection].description }}</span>
                    </p>
                </div>

                <!-- Static content - no animation -->
                <div class="gap-4 pt-2 hidden md:flex">
                    <button class="bg-white text-black px-4 py-2 rounded font-semibold">Book a call</button>
                    <button class="bg-transparent text-white border border-gray-300 px-4 py-2 rounded font-semibold">
                        Contact us
                    </button>
                </div>
            </div>
        </div>

        <!-- Right chat window with carousel -->
        <div class="lg:absolute relative lg:right-20 lg:top-1/2 lg:-translate-y-1/2 w-full lg:max-w-[450px] mx-auto px-4 lg:px-0 pb-12 md:pb-24 lg:pb-0"
            @mouseenter="pause = true" @mouseleave="pause = false" @touchstart="startTouch($event)"
            @touchend="endTouch($event)">
            <div
                class="w-fullh-[300px] sm:h-[450px] lg:h-[600px] bg-gray-50 rounded shadow-xl flex items-center justify-center chat-window">
                <div :key="activeSection"
                    class="flex flex-col justify-center gap-4 text-base w-full max-w-xl mx-auto px-4 py-6 h-full overflow-y-auto">
                    <div v-for="(msg, i) in sections[activeSection]" :key="i"
                        :class="msg.from === 'user' ? 'flex justify-start' : 'flex justify-end'"
                        class="transition-all duration-300" :style="{
                    opacity: shouldShowMessage(i, msg) ? 1 : 0,
                    transform: shouldShowMessage(i, msg) ? 'translateY(0)' : 'translateY(10px)',
                    transitionDelay: shouldShowMessage(i, msg) ? `${i * 300}ms` : '0ms'
                }">
                        <!-- Regular text message -->
                        <div v-if="!msg.type" :class="['chat-bubble', msg.from === 'user' ? 'from' : 'to']">
                            {{ msg.text }}
                        </div>

                        <!-- Image message with typing indicator -->
                        <div v-else class="chat-bubble to">
                            <div v-if="showTypingIndicator(i)" class="typing-indicator" aria-hidden="true">
                                <span></span><span></span><span></span>
                            </div>
                            <div v-else
                                class="rounded-xl w-full max-w-[180px] h-[120px] flex items-center justify-center">
                                <ImageIcon class="h-28 w-28 text-gray-500" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- Carousel Dots - Styled like the image -->
            <div class="flex justify-center mt-2 pt-2">
                <div class="carousel-dots-container rounded">
                    <span v-for="(s, i) in sectionInfo.length" :key="i" @click="goTo(i)" class="carousel-dot"
                        :class="i === activeSection ? 'active' : ''"></span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue';
import { ImageIcon, ChevronLeft, ChevronRight } from 'lucide-vue-next';

const activeSection = ref(0);
const pause = ref(false);
const isTransitioning = ref(false);
const animatedChatIndex = ref(-1);
const typingIndicatorIndex = ref(-1);
let interval = null;
let touchStartX = 0;
let chatAnimationTimer = null;
let typingIndicatorTimer = null;

// Helper function to determine if a message should be shown
const shouldShowMessage = (index, msg) => {
    if (msg.type === 'image') {
        return typingIndicatorIndex.value >= index || animatedChatIndex.value >= index;
    } else {
        return animatedChatIndex.value >= index;
    }
};

// Helper function to determine if typing indicator should be shown
const showTypingIndicator = (index) => {
    return typingIndicatorIndex.value === index;
};

const goTo = (index) => {
    if (index < 0 || index >= sectionInfo.length) return;
    transitionTo(index);
};

const next = () => {
    transitionTo((activeSection.value + 1) % sectionInfo.length);
};

const prev = () => {
    transitionTo((activeSection.value - 1 + sectionInfo.length) % sectionInfo.length);
};

const transitionTo = (index) => {
    isTransitioning.value = true;
    animatedChatIndex.value = -1;
    typingIndicatorIndex.value = -1;

    // Clear any existing timers
    if (chatAnimationTimer) {
        clearTimeout(chatAnimationTimer);
    }
    if (typingIndicatorTimer) {
        clearTimeout(typingIndicatorTimer);
    }

    setTimeout(() => {
        activeSection.value = index;
        isTransitioning.value = false;

        // Start chat animation sequence
        startChatAnimation();
    }, 400);
};

const startChatAnimation = () => {
    // Reset animation index
    animatedChatIndex.value = -1;
    typingIndicatorIndex.value = -1;

    // Animate each chat bubble with a delay
    const currentSectionMessages = sections[activeSection.value];
    const animateNextBubble = (index) => {
        if (index < currentSectionMessages.length) {
            const currentMsg = currentSectionMessages[index];

            if (currentMsg.from === 'image') {
                // For image messages, show typing indicator first
                typingIndicatorIndex.value = index;

                // After 1.5 seconds, show the actual image
                typingIndicatorTimer = setTimeout(() => {
                    typingIndicatorIndex.value = -1;
                    animatedChatIndex.value = index;

                    // Move to next message after image appears
                    chatAnimationTimer = setTimeout(() => {
                        animateNextBubble(index + 1);
                    }, 600);
                }, 1500);
            } else {
                // For text messages, show immediately
                animatedChatIndex.value = index;
                chatAnimationTimer = setTimeout(() => {
                    animateNextBubble(index + 1);
                }, 600); // 600ms between each message
            }
        }
    };

    // Start the animation sequence
    setTimeout(() => {
        animateNextBubble(0);
    }, 200);
};

const startTouch = (e) => {
    touchStartX = e.changedTouches[0].clientX;
};

const endTouch = (e) => {
    const deltaX = e.changedTouches[0].clientX - touchStartX;
    if (Math.abs(deltaX) > 50) {
        deltaX > 0 ? prev() : next();
    }
};

onMounted(() => {
    // Start the initial chat animation
    startChatAnimation();

    // Set up auto-advance interval
    interval = setInterval(() => {
        if (!pause.value) next();
    }, 10000); // Increased to 10 seconds to allow for chat and typing animations
});

onUnmounted(() => {
    if (interval) clearInterval(interval);
    if (chatAnimationTimer) clearTimeout(chatAnimationTimer);
    if (typingIndicatorTimer) clearTimeout(typingIndicatorTimer);
});

// Watch for active section changes to restart chat animation
watch(activeSection, () => {
    startChatAnimation();
});

const sectionInfo = [
    { title: 'Business Use Case', description: 'Explore the initial idea and find real-world validation.' },
    { title: 'Positioning Strategy', description: 'Stand out in a crowded market with the right message.' },
    { title: 'Business Strategy', description: 'Get a clear go-to-market and growth plan.' },
    { title: 'Pricing Dilemma', description: "Let's figure out a pricing model that works." },
    { title: 'Pitch Deck', description: 'Present your vision to investors with confidence.' },
    { title: 'Logo Design', description: "We'll craft a memorable brand identity." },
    { title: 'Brand Identity', description: 'Fonts, tone, colors — all aligned and consistent.' },
    { title: 'UI Design', description: 'Make your product feel clean and professional.' },
    { title: 'Landing Page', description: 'Convert visitors into believers.' },
    { title: 'App Vision', description: 'Turn your product dreams into wireframes.' },
    { title: 'Digital Storefront', description: 'Sell products with a user-friendly layout.' },
    { title: 'Social Strategy', description: 'Know what to say — and when to say it.' },
    { title: 'Design Templates', description: 'Branded content that feels pro — every time.' },
    { title: 'Posting System', description: 'Keep your social consistent and effortless.' },
    { title: 'Lead Generation', description: 'Turn attention into traction through ads.' },
    { title: 'Success Milestone', description: 'Celebrate the journey. You made it!' }
];

const sections = [
    [
        { from: 'user', text: 'I\'ve had this idea in my head forever…\nBut I\'m not even sure if people actually need it.' },
        { from: 'vismaya', text: 'Let us dig into that.\nGive us a bit of time to run the market research. Say less.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'I just don\'t know how to position this.\nIt feels like everyone\'s already doing it…' },
        { from: 'vismaya', text: 'We\'ll work on a positioning angle that makes you stand out.\nGive us a day to draft it. We got you.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'Honestly… I don\'t have a solid business strategy.' },
        { from: 'vismaya', text: 'No problem — we\'ll sketch a launch roadmap and growth plan.\nGive us some time to map it clearly.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'I\'m stuck on pricing.\nToo low feels wrong, too high feels risky.' },
        { from: 'vismaya', text: 'Let us run some value analysis and market check.\nWe\'ll share a pricing suggestion soon.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'If I want to raise funds later, I\'ll need a pitch deck too…' },
        { from: 'vismaya', text: 'Leave that to us.\nWe\'ll start building something clean and convincing. Give us a few days.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'Still haven\'t found the right logo…' },
        { from: 'vismaya', text: 'We\'ll sketch out a few directions.\nLet us put together a few concepts for you to review.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'Fonts, colors, tone — I keep changing everything.' },
        { from: 'vismaya', text: 'We\'ll prepare a proper brand guide.\nNeed a bit of time, but it\'ll lock everything in place.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'I\'ve tried designing the site… it just doesn\'t feel right.' },
        { from: 'vismaya', text: 'Let us clean up the UI and layout.\nGive us a couple days and we\'ll show you something solid.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'I need a landing page — but not just something pretty. It has to convert.' },
        { from: 'vismaya', text: 'We hear you.\nWe\'ll draft the copy and layout — give us a bit to fine-tune it.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'Might want an app someday too…' },
        { from: 'vismaya', text: 'We can sketch out the app flow for you.\nLet us work on the wireframe first.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'Thinking of selling stuff later — digital products maybe?' },
        { from: 'vismaya', text: 'Let\'s prep a store layout and product structure.\nWe\'ll send something soon.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'I have no clue what to post on social…' },
        { from: 'vismaya', text: 'We\'ll build a content plan around your brand.\nGive us a short brief — we\'ll take care of the rest.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'But I\'m not a designer… the posts never look good.' },
        { from: 'vismaya', text: 'No worries.\nWe\'ll design a batch of branded templates for you — just need a little time.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'Also… I can\'t keep up with posting.' },
        { from: 'vismaya', text: 'Let us handle that.\nWe\'ll organize the posting routine — just give us access.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'Likes are cool but… I really need leads.' },
        { from: 'vismaya', text: 'We\'ll set up your first ad campaign.\nGive us a few days to prepare the copy, creative, and targeting.' },
        { from: 'vismaya', type: 'image' }
    ],
    [
        { from: 'user', text: 'Hey… just wanted to say thank you.\nWe\'re now doing over $20K MRR — and it all started with that first call with you.' },
        { from: 'vismaya', text: 'Let\'s gooo.\nYou did the scary part — we just helped you move. Proud of you.' }
    ]
];
</script>

<style scoped>
.chat-bubble {
    max-width: 80%;
    padding: 0.75rem 1rem;
    line-height: 1.5;
    border-radius: 8px;
    position: relative;
    word-wrap: break-word;
    width: fit-content;
    white-space: pre-line;
}

.chat-bubble.from {
    align-self: flex-start;
    background: #FEFFFF;
    border: 1px solid #e5e7eb;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.06);
}

.chat-bubble.from::after {
    content: '';
    position: absolute;
    left: -8px;
    bottom: 10px;
    border-top: 8px solid transparent;
    border-right: 8px solid #fff;
}

.chat-bubble.to {
    align-self: flex-end;
    background: #E2FFC7;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.06);
}

.chat-bubble.to::after {
    content: '';
    position: absolute;
    right: -8px;
    bottom: 10px;
    border-top: 8px solid transparent;
    border-left: 8px solid #f3f4f6;
}

/* Chat window with WhatsApp background */
.chat-window {
    background-image: url('/src/assets/whatsapp-background.png');
    background-repeat: repeat;
    background-size: 410px;
    background-position: center;
    overflow: hidden;
}

/* Carousel dots styling to match the image */
.carousel-dots-container {
    display: flex;
    align-items: center;
    gap: 6px;
}

.carousel-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 0.3s ease;
}

.carousel-dot.active {
    width: 24px;
    border-radius: 10px;
    background-color: white;
}

/* Carousel arrows styling to match the image */
.carousel-arrow {
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: white;
    border-radius: 50%;
    cursor: pointer;
    transition: all 0.2s ease;
    border: none;
    outline: none;
    color: black;
}

.carousel-arrow:hover {
    background-color: rgba(255, 255, 255, 0.9);
    transform: scale(1.05);
}

/* Dynamic content animations */
.dynamic-content {
    transition: all 0.4s ease;
}

/* Typing indicator animation */
.typing-indicator {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 12px 16px;
    height: 40px;
    width: 64px;
}

.typing-indicator span {
    height: 8px;
    width: 8px;
    margin: 0 2px;
    background-color: #000000;
    border-radius: 50%;
    display: inline-block;
    opacity: 0.4;
}

.typing-indicator span:nth-child(1) {
    animation: typing 1.2s infinite ease-in-out;
    animation-delay: 0s;
}

.typing-indicator span:nth-child(2) {
    animation: typing 1.2s infinite ease-in-out;
    animation-delay: 0.2s;
}

.typing-indicator span:nth-child(3) {
    animation: typing 1.2s infinite ease-in-out;
    animation-delay: 0.4s;
}

@keyframes typing {
    0% {
        transform: translateY(0);
        opacity: 0.4;
    }

    50% {
        transform: translateY(-10px);
        opacity: 1;
    }

    100% {
        transform: translateY(0);
        opacity: 0.4;
    }
}
</style>