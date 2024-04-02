<script setup>
import { useDateFormat, useNow } from '@vueuse/core'

const currentTime = useDateFormat(useNow(), 'hh:mm A')

const closeOS = () => {
  window.close()
}
</script>

<template>
  <div class="Taskbar">
    <div class="powerButton" @click="closeOS">
      <img draggable="false" src="/Media/powerButton.webp" alt="Power off Button" />
    </div>
    <div class="ActiveAppsWrapper"></div>
    <div class="Time">
      {{ currentTime }}
    </div>
  </div>
</template>

<style scoped>
.Taskbar {
  box-sizing: border-box;
  flex: 1;
  background-color: var(--gray);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px 10px;
}

img {
  height: 100%;
}

.powerButton {
  aspect-ratio: 1 / 1;
  height: 90%;
}

.powerButton:hover {
  cursor: pointer;
}

.powerButton:active {
  scale: 0.8;
}

.Time {
  height: fit-content;
  padding: 5px 10px;
  font-size: var(--dateSize);
  border: 2px solid black;
  box-shadow: 2px 2px 0px 2px var(--darkGray);
}
</style>
