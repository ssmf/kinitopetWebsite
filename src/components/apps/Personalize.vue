<script setup>
import { ref } from 'vue'

const wallpaperPaths = Object.keys(import.meta.glob('/public/Media/Wallpapers/*'))

const colorList = [
  { mainColor: '#807e7e', secondaryColor: '#c3c3c3' },
  { mainColor: '#0500ff', secondaryColor: '#03afff' },
  { mainColor: '#7b0000', secondaryColor: '#ce3030' },
  { mainColor: '#116309', secondaryColor: '#1cdf0b' }
]

const currentColor = ref(colorList[0])

const getSRC = (src) => {
  return new URL(src.replace('/public', ''), import.meta.url).href
}
</script>

<template>
  <div class="Personalize col">
    <div class="Themes">
      <h1>Themes:</h1>
      <div class="ThemeList row">
        <button
          class="ThemeButton"
          v-for="clr in colorList"
          :key="JSON.stringify(clr)"
          :style="{
            backgroundColor: clr.mainColor,
            boxShadow: `3px 3px 0px 3px ${clr.secondaryColor}`
          }"
          @click="currentColor = clr"
        ></button>
      </div>
    </div>
    <div class="Wallpapers col">
      <h1>Wallpapers:</h1>
      <div class="WallpapersList row">
        <img :src="getSRC(wlp)" v-for="wlp in wallpaperPaths" :key="JSON.stringify(wlp)" />
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  width: 100%;
}

img {
  width: 192px;
  height: 108px;
  cursor: pointer;
  border: 1px solid black;
}

.WallpapersList {
  width: 600px;
  flex-wrap: wrap;
  gap: 10px;
}

.Personalize {
  gap: 40px;
}

.Themes {
  width: 100%;
}

.ThemeButton {
  border: 2px solid black;
  width: 64px;
  height: 64px;
  background-color: var(--seaColor);
  box-shadow: 2px 2px 0px 2px var(--gray);
  cursor: pointer;
}

.ThemeList {
  width: 100%;
  justify-content: space-around;
}
</style>
