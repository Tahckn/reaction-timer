<template>
  <header>
    <h1>Reaction Timer</h1>
  </header>
  <main>
    <button :disabled="data.isPlaying" @click="start">Play</button>
    <Block v-if="data.isPlaying" :delay="data.delayArray" @end="endGame" />
    <Results v-if="data.showResults" :scores="data.scoreArray" />
  </main>
</template>

<script setup>
import Block from './components/Block.vue'
import Results from './components/Results.vue'
import { reactive } from 'vue'

const data = reactive({
  isPlaying: false,
  delay: 0,
  delayArray: [],
  emittedScore: null,
  showResults: false,
  scoreArray: [],
})

const start = () => {
  data.isPlaying = true
  data.delay = 2000 + Math.random() * 5000
  data.delayArray.unshift(data.delay)
  data.showResults = false
}

const endGame = (reactionTime) => {
  data.emittedScore = reactionTime ?? '0'
  data.isPlaying = false
  data.showResults = true
  data.scoreArray.unshift(data.emittedScore)
}
</script>

<style>
header {
  margin: 0 auto;
}

h1 {
  font-weight: bold;
}

button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 15px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
  transition: transform 0.3s ease-in-out;
}

button:hover {
  transform: scale(1.05);
  box-shadow: 0 0 10px #0faf87;
}

button:active {
  transform: scale(0.9);
}

button:disabled {
  opacity: 0.2;
  cursor: not-allowed;
  transform: scale(1);
  box-shadow: none;
}
</style>
