<template>
    <div class="w-full max-w-lg aspect-square overflow-hidden flex flex-col">
        <!-- Game Content -->
        <div class="flex-grow flex flex-col p-4">
            <!-- Game Info -->
            <div class="bg-white border border-gray-300 rounded p-3 mb-4 text-center">
                <p class="font-bold text-lg mb-2">Round {{ currentRound }} / 3</p>
                <p class="text-gray-600">Player: {{ playerScore }} | Computer: {{ computerScore }}</p>
            </div>

            <!-- Battle Scene -->
            <div class="flex justify-between items-center mb-6 h-32">
                <!-- Player's Choice -->
                <div class="flex flex-col items-center">
                    <transition name="fade-in-out" mode="out-in">
                        <div v-if="playerChoice" :key="playerChoice" class="text-center">
                            <component :is="getIcon(playerChoice)" :size="64" class="text-teal-500 animate-bounce" />
                        </div>
                    </transition>
                    <p class="mt-2 text-sm text-gray-700">Player</p>
                </div>

                <!-- VS Text -->
                <div class="flex items-center justify-center text-2xl font-bold text-gray-600">
                    VS
                </div>

                <!-- Computer's Choice -->
                <div class="flex flex-col items-center">
                    <transition name="fade-in-out" mode="out-in">
                        <div v-if="computerChoice" :key="computerChoice" class="text-center">
                            <component :is="getIcon(computerChoice)" :size="64" class="text-red-500 animate-bounce" />
                        </div>
                    </transition>
                    <p class="mt-2 text-sm text-gray-700">Computer</p>
                </div>
            </div>

            <!-- Move Selection -->
            <div v-if="currentRound <= 3" class="mt-auto">
                <p class="text-center font-bold mb-3 text-gray-800">Choose your move:</p>
                <div class="flex justify-center space-x-4">
                    <button v-for="choice in choices" :key="choice" @click="playRound(choice)"
                        class="px-4 py-2 bg-teal-500 text-white rounded-lg shadow hover:bg-teal-600 transition-all transform hover:scale-105 font-bold">
                        {{ choice }}
                    </button>
                </div>
            </div>

            <!-- Game Over Section -->
            <div v-else class="mt-auto text-center">
                <p class="text-2xl font-bold mb-2 text-gray-800">Battle Over!</p>
                <p class="text-lg mb-4 text-teal-600 font-semibold">Your Discount: {{ discount }}%</p>
                <button @click="resetGame"
                    class="px-6 py-3 bg-teal-500 text-white rounded-lg shadow hover:bg-teal-600 transition-all transform hover:scale-105 font-bold">
                    New Battle
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { Grab, Hand, Scissors } from 'lucide-vue-next'

const choices = ['Rock', 'Paper', 'Scissors']
const currentRound = ref(1)
const playerScore = ref(0)
const computerScore = ref(0)
const battleLog = ref([])
const playerChoice = ref(null)
const computerChoice = ref(null)

const discount = computed(() => {
    if (playerScore.value === 3) return 50
    if (playerScore.value === 2) return 20
    if (playerScore.value === 1) return 10
    return 0
})

function getIcon(choice) {
    switch (choice) {
        case 'Rock': return Grab
        case 'Paper': return Hand
        case 'Scissors': return Scissors
        default: return null
    }
}

function getComputerChoice() {
    return choices[Math.floor(Math.random() * choices.length)]
}

function determineWinner(player, computer) {
    if (player === computer) return 'Tie'
    if (
        (player === 'Rock' && computer === 'Scissors') ||
        (player === 'Paper' && computer === 'Rock') ||
        (player === 'Scissors' && computer === 'Paper')
    ) {
        return 'Player'
    }
    return 'Computer'
}

function playRound(playerMove) {
    playerChoice.value = playerMove
    const computerMove = getComputerChoice()
    computerChoice.value = computerMove
    const roundWinner = determineWinner(playerMove, computerMove)

    if (roundWinner === 'Player') {
        playerScore.value++
        battleLog.value.unshift(`You win! ${playerMove} beats ${computerMove}`)
    } else if (roundWinner === 'Computer') {
        computerScore.value++
        battleLog.value.unshift(`You lose! ${computerMove} beats ${playerMove}`)
    } else {
        battleLog.value.unshift(`It's a tie! Both chose ${playerMove}`)
    }

    currentRound.value++

    // Reset choices after a short delay
    setTimeout(() => {
        playerChoice.value = null
        computerChoice.value = null
    }, 1500)
}

function resetGame() {
    currentRound.value = 1
    playerScore.value = 0
    computerScore.value = 0
    battleLog.value = []
    playerChoice.value = null
    computerChoice.value = null
}
</script>

<style scoped>
.fade-in-out-enter-active,
.fade-in-out-leave-active {
    transition: opacity 0.5s ease;
}

.fade-in-out-enter-from,
.fade-in-out-leave-to {
    opacity: 0;
}

.fade-up-enter-active,
.fade-up-leave-active {
    transition: all 0.5s ease;
}

.fade-up-enter-from,
.fade-up-leave-to {
    opacity: 0;
    transform: translateY(30px);
}

@keyframes bounce {

    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-10px);
    }
}

.animate-bounce {
    animation: bounce 1s infinite;
}
</style>