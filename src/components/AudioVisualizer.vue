<script setup>
import { onMounted, ref } from 'vue'

const analyzer = defineModel('analyzer')

const bufferLength = analyzer.value.frequencyBinCount
const dataArr = new Uint8Array(bufferLength)

setInterval(() => {
  console.log(analyzer.value)
}, 1000)

const visualizerCanvas = ref(null)
let ctx = null
let barWidth = 0
let barHeight = 0

onMounted(() => {
  ctx = visualizerCanvas.value.getContext('2d', { antialias: false })
  barWidth = (visualizerCanvas.value.width * 1.3) / bufferLength
  animateBars()
})

let x = 0

const animateBars = () => {
  x = 0
  ctx.clearRect(0, 0, visualizerCanvas.value.width, visualizerCanvas.value.height)
  analyzer.value.getByteFrequencyData(dataArr)
  for (let i = 0; i < bufferLength; i++) {
    barHeight = dataArr[i]
    if (i % 2 == 0) {
      ctx.fillStyle = 'black'
    } else {
      ctx.fillStyle = '#f3b2f8'
    }
    ctx.fillRect(x, visualizerCanvas.value.height - barHeight * 0.6, barWidth, barHeight)
    x += barWidth
  }

  requestAnimationFrame(animateBars)
}
</script>

<template>
  <div class="AudioVisualizer">
    <canvas class="VisualizerContent" ref="visualizerCanvas"></canvas>
  </div>
</template>

<style scoped>
.AudioVisualizer {
  width: 100%;
  height: 200px;
  background-color: var(--darkGray);
  border: 7px solid var(--gray);
}

.VisualizerContent {
  height: 100%;
  width: 100%;
}
</style>
