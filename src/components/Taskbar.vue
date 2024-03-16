<script setup>
import { useDateFormat, useNow } from '@vueuse/core'

const currentTime = useDateFormat(useNow(), 'HH:mm A')
</script>

<template>
  <div class="Taskbar">
    <div class="powerButton">
      <img src="/public/Assets/Media/powerButton.webp" alt="Power off Button" />
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
  border: 5px solid white;
  border-bottom: none;
}

img {
  height: 100%;
}

.powerButton {
  height: 100%;
  width: fit-content;
  padding: 10px;
}

.powerButton:hover {
  cursor: pointer;
}

.powerButton:active {
  padding: 15px;
}

.Taskbar {
  flex: 1;
  background-color: var(--gray);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0px 10px;
}

.Time {
  height: fit-content;
  padding: 5px 10px;
  font-size: var(--dateSize);
  border: 4px solid black;
  box-shadow: 4px 4px 0px 2px var(--darkGray);
}
</style>
