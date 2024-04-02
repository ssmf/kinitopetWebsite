<script setup>
import Desktop from '@/components/Desktop.vue'
import Taskbar from '@/components/Taskbar.vue'
import { onMounted, ref } from 'vue'
const isLoading = ref(true)
const finishedLoaing = ref(false)

onMounted(() => {
  const num = 1000 * Math.floor(Math.random() * (5 - 2 + 1) + 2)
  setTimeout(() => {
    isLoading.value = false
  }, num)
  setTimeout(() => {
    finishedLoaing.value = true
  }, num + 2000)
})
</script>

<template>
  <div class="main">
    <Desktop></Desktop>
    <Taskbar></Taskbar>
  </div>
  <div v-if="!finishedLoaing" class="LoadingScreen col" :class="{ FinishedLoadingOS: !isLoading }">
    <img src="/public/Media/KinitoOSLoading.webp" class="LoadingScreenImage" />
    <div class="LoadingBar">
      <div class="BarProgressWrapper row">
        <div class="BarProgress"></div>
        <div class="BarProgress"></div>
        <div class="BarProgress"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.LoadingScreen {
  position: fixed;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 3;
  background-color: black;
  opacity: 1;
  transition: 2s all ease-in-out;
}

div > .FinishedLoadingOS {
  opacity: 0;
}

.LoadingScreen {
  gap: 20px;
}

.LoadingScreenImage {
  height: 256px;
  width: auto;
  mix-blend-mode: lighten;
}

.LoadingBar {
  border: 2px solid var(--gray);
  width: 300px;
  height: 20px;
  border-radius: 5px;
  overflow: hidden;
}

@keyframes moveBars {
  from {
    margin-left: -50px;
  }
  to {
    margin-left: 350px;
  }
}

.BarProgressWrapper {
  animation: moveBars 4s steps(20, end) infinite;
  width: 20%;
  height: 100%;
  gap: 4px;
  padding: 2px 2px;
}

.BarProgress {
  width: 30%;
  height: 100%;
  border-radius: 3px;
  background-color: var(--seaColor);
}

.main {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: stretch;
}
</style>
