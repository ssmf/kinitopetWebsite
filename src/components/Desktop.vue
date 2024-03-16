<script setup>
import { onMounted, ref } from 'vue'
import File from '@/components/File.vue'

const Files = ref([
  { name: 'MyComputer', fileExtension: 'webp', iconScale: 0.9 },
  { name: 'MusicPlayer', fileExtension: 'webp', iconScale: 1.5 }
])
let openWindows = []
let currentSelection = null
const DesktopDom = ref(null)

let Openable = false
let isDragging = false

const Select = (newSel) => {
  isDragging = true

  currentSelection = newSel
  currentSelection.classList.add('Overlay')
}

const UnSelect = (fileDom) => {
  console.log('Unselected!')
  document.getElementById(fileDom).classList.remove('Overlay')
}

window.addEventListener('mouseup', () => {
  if (isDragging) {
    isDragging = false
  }
})
</script>

<template>
  <div class="Desktop" id="Desktop" ref="DesktopDom">
    <File
      v-for="specificFile in Files"
      :key="specificFile.name"
      :Name="specificFile.name"
      :IconPath="specificFile.name + '.' + specificFile.fileExtension"
      :iconScale="specificFile.iconScale"
      :id="specificFile.name"
      v-model:selectFunction="Select"
      v-model:UnSelect="UnSelect"
    >
    </File>
  </div>
</template>

<style scoped>
.Desktop {
  flex: 13;
  padding: 12px;
  background-image: url('/public/Assets/Media/DefaultWallpaper.webp');
  background-size: cover;
  background-position: center;
  image-rendering: crisp-edges;

  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
  grid-template-rows: repeat(auto-fill, 100px);
  grid-auto-flow: column;
  gap: 25px;
  position: relative;
}

.Selected {
  filter: drop-shadow(0p 0px 10px blue);
}

.Overlay::before {
  height: 100%;
  width: 100%;
  background-color: blue;
  opacity: 0.8;
}
</style>
