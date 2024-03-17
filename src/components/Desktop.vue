<script setup>
import { onMounted, ref } from 'vue'
import File from '@/components/File.vue'
import { useMouse, useElementSize } from '@vueuse/core'

const Files = ref([
  { name: 'MyComputer', fileExtension: 'webp', iconScale: 0.9 },
  { name: 'MusicPlayer', fileExtension: 'webp', iconScale: 1.5 }
])
let openWindows = []
let currentSelection = null
const DesktopDom = ref(null)
const mousePos = ref(useMouse())

let Openable = false
let isDragging = false

const Select = (newSel) => {
  isDragging = true

  currentSelection = newSel
  currentSelection.classList.add('Dragging')
  currentSelection.style.gridArea = 0 / 0 / 0 / 0
  currentSelection.classList.add('Overlay')
  console.log('Holding')
}

const UnSelect = (fileDom) => {
  document.getElementById(fileDom).classList.remove('Overlay')
}

window.addEventListener('mouseup', () => {
  if (isDragging) {
    isDragging = false
    console.log('Not holding')
    currentSelection.classList.remove('Dragging')
    PlaceFile()
  }
})

const PlaceFile = () => {
  const DesktopSize = useElementSize(DesktopDom)
  const maxX = Math.floor(DesktopSize.width.value / 120 + 1)
  const maxY = Math.floor(DesktopSize.height.value / 120)

  const x = clampFunc(Math.floor(mousePos.value.x / 120) + 1, maxX)
  const y = clampFunc(Math.floor(mousePos.value.y / 120) + 1, maxY)

  console.log(x)

  currentSelection.style.gridArea = `${y} / ${x} / ${y + 1} / ${x + 1}`
}

const clampFunc = (val, max) => {
  return val > max ? max : val
}
</script>

<template>
  <div class="Desktop" id="Desktop" ref="DesktopDom">
    <File
      :style="`top: ${mousePos.y - 50}px; left: ${mousePos.x - 50}px;`"
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
  gap: 20px;
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

div > .Dragging {
  position: absolute;
  width: 100px;
  height: 100px;
}
</style>
