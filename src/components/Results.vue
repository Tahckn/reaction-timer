<template>
  <div class="wrapper">
    <p>Reaction time - {{ props.scores[0] }}ms</p>
    <p class="rank" :class="classObject">{{ data.rank }}</p>
  </div>
</template>

<script setup>
import { reactive, onMounted } from 'vue'

const data = reactive({
  rank: null,
})

const classObject = reactive({
  lightning: false,
  super: false,
  very: false,
  fast: false,
  average: false,
  slow: false,
  veryslow: false,
})

const props = defineProps({
  scores: Array,
})

onMounted(() => {
  if (props.scores[0] < 200) {
    data.rank = 'Lightning fast'
    classObject.lightning = true
  } else if (props.scores[0] >= 200 && props.scores[0] < 300) {
    data.rank = 'Super fast'
    classObject.super = true
  } else if (props.scores[0] >= 300 && props.scores[0] < 400) {
    data.rank = 'Very fast'
    classObject.very = true
  } else if (props.scores[0] >= 400 && props.scores[0] < 500) {
    data.rank = 'Fast'
    classObject.fast = true
  } else if (props.scores[0] >= 500 && props.scores[0] < 750) {
    data.rank = 'Average'
    classObject.average = true
  } else if (props.scores[0] >= 750 && props.scores[0] < 1000) {
    data.rank = 'Slow'
    classObject.slow = true
  } else {
    data.rank = 'Very Slow'
    classObject.veryslow = true
  }
})
</script>

<style>
h3 {
  font-weight: bold;
}
.rank {
  font-size: 1.4em;
  font-weight: bold;
}

.rank.lightning {
  color: rgb(90, 255, 128);
}
.rank.super {
  color: rgb(72, 204, 102);
}
.rank.very {
  color: rgb(54, 153, 76);
}
.rank.fast {
  color: rgb(36, 101, 50);
}
.rank.average {
  color: 'rgb(151, 152, 175)';
}
.rank.slow {
  color: rgb(124, 29, 22);
}
.rank.veryslow {
  color: rgb(252, 60, 47);
}
</style>
