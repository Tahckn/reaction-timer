<template>
  <div class="block" v-if="data.showBlock" @click="stopTimer">click me</div>
</template>

<script setup>
import { onMounted, reactive, defineEmits } from 'vue'

const emit = defineEmits(['end'])

const data = reactive({
  showBlock: false,
  timer: null,
  reactionTime: null,
})

onMounted(() => {
  setTimeout(() => {
    data.showBlock = true
    startTimer()
  }, props.delay[0])
})

const props = defineProps({
  delay: Array,
})

const startTimer = () => {
  data.timer = setInterval(() => {
    data.reactionTime += 10
  }, 10)
}

const stopTimer = () => {
  clearInterval(data.timer)
  emit('end', data.reactionTime)
}
</script>

<style scoped>
.block {
  width: 400px;
  border-radius: 15px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>
