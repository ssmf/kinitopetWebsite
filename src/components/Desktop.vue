<script setup>
import { ref, provide } from 'vue'
import File from '@/components/File.vue'
import { useMouse, useElementSize, until } from '@vueuse/core'
import AppWindow from './AppWindow.vue'

const currentTheme = ref({ mainColor: '#807e7e', secondaryColor: '#c3c3c3' })
const currentWallpaper = ref('/public/Media/Wallpapers/Wallpaper1.webp')

const changeTheme = (newTheme) => {
  currentTheme.value = newTheme
}

const changeWallpaper = (newWallpaper) => {
  currentWallpaper.value = newWallpaper
  console.log(currentWallpaper.value)
}

provide('currentTheme', {
  currentTheme,
  changeTheme
})

provide('currentWallpaper', {
  currentWallpaper,
  changeWallpaper
})

const Files = ref([
  { name: 'My Computer', fileExtension: 'webp', iconScale: 0.9 },
  { name: 'Audio Player', fileExtension: 'webp', iconScale: 1.5 },
  { name: 'About Kinitopet', fileExtension: 'webm', iconScale: 1.5 },
  { name: 'Character Details', fileExtension: 'webp', iconScale: 0.8 },
  { name: 'Paint', fileExtension: 'webp', iconScale: 1.3 },
  { name: 'Terminal', fileExtension: 'webm', iconScale: 0.8 },
  { name: 'Author', fileExtension: 'webp', iconScale: 0.8 },
  { name: 'About me', fileExtension: 'webp', iconScale: 1 },
  { name: 'Personalize', fileExtension: 'webp', iconScale: 1 },
  { name: 'Settings', fileExtension: 'webp', iconScale: 0.85 },
  { name: 'Images', fileExtension: 'webp', iconScale: 0.9 }
])

const GenerateRandomString = (length) => {
  const characters = 'QWERTYUIOPASDFGHJKLZXCVBNM1234567890'
  let generatedString = ''
  for (let i = 0; i < length; i++) {
    generatedString += characters.charAt(Math.floor(Math.random() * characters.length))
  }
  return generatedString
}

const ComputerSpecs = ref({
  DiskSpace: Math.floor((Math.random() * (6 - 2) + 2) * 10) / 10,
  DiskSpaceTaken: 1 + Math.floor(Math.random() * 100) / 100,
  LicenseValidationTime: Math.floor(Math.random() * (45 - 12) + 12),
  DeviceName: '1L0V3K1N1T0P3T369',
  CPU: 'K386-32',
  RAM: Math.floor(Math.random() * (8 - 6) + 6),
  OsType: '32-bit (k-bit)',
  OsBuild: GenerateRandomString(25),
  DeviceId: 'K1NIT0PC-' + GenerateRandomString(4) + '000401',
  FileCount: Files.value.length
})

const SessionTime = ref(0)
setInterval(() => {
  SessionTime.value++
}, 1000)

let openWindows = ref([])
let currentSelection = null
const DesktopDom = ref(null)
const mousePos = ref(useMouse())

let Openable = false
let isDragging = false

const Select = async (newSel) => {
  if (
    currentSelection == newSel &&
    Openable &&
    !openWindows.value.find((e) => e == currentSelection.id)
  ) {
    openWindows.value.push(currentSelection.id)
  }

  isDragging = true
  Openable = true
  currentSelection = newSel
  currentSelection.classList.add('Overlay')

  setTimeout(() => {
    Openable = false
  }, 500)

  await until(mousePos.value).changed()
  if (isDragging) {
    currentSelection.classList.add('Dragging')
  }
}

const UnSelect = (fileDom) => {
  document.getElementById(fileDom).classList.remove('Overlay')
}

window.addEventListener('mouseup', () => {
  if (isDragging) {
    isDragging = false
    currentSelection.classList.remove('Dragging')
    PlaceFile()
  }
})

const PlaceFile = () => {
  const DesktopSize = useElementSize(DesktopDom)
  let isTaken = false
  const maxX = Math.floor(DesktopSize.width.value / 120 + 1) - 1
  const maxY = Math.floor(DesktopSize.height.value / 120)

  const x = clampFunc(Math.floor(mousePos.value.x / 120) + 1, maxX)
  const y = clampFunc(Math.floor(mousePos.value.y / 120) + 1, maxY)

  DesktopDom.value.childNodes.forEach((file) => {
    if (file.style && file.style.gridArea == `${y} / ${x} / ${y + 1} / ${x + 1}`) {
      console.log('This area is taken!')
      isTaken = true
      return 0
    }
  })
  if (!isTaken) {
    currentSelection.style.gridArea = `${y} / ${x} / ${y + 1} / ${x + 1}`
  }
}

const clampFunc = (val, max) => {
  return val > max ? max : val
}

const closeWindow = (window) => {
  console.log('closed')
  openWindows.value = openWindows.value.filter((el) => el != window)
}

const putOnTop = (window) => {
  const newArr = openWindows.value.filter((el) => el != window)
  newArr.push(window)
  openWindows.value = newArr
}

const getSRC = (src) => {
  console.log(src)
  return new URL(src.replace('/public', ''), import.meta.url).href
}
</script>

<template>
  <div
    class="Desktop"
    id="Desktop"
    ref="DesktopDom"
    :style="{ backgroundImage: `url(${getSRC(currentWallpaper)})` }"
  >
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
  <div class="OpenWindowsWrapper">
    <AppWindow
      v-for="appWindow in openWindows"
      :key="JSON.stringify(appWindow)"
      :Name="appWindow"
      :MousePos="mousePos"
      :ComputerSpecs="ComputerSpecs"
      v-model:closeFunc="closeWindow"
      v-model:putOnTop="putOnTop"
      v-model:SessionTime="SessionTime"
      :IconExtension="Files.find((e) => e.name == appWindow).fileExtension"
      :IconScale="Files.find((e) => e.name == appWindow).iconScale"
    ></AppWindow>
  </div>
</template>

<style scoped>
.Desktop {
  flex: 13;
  padding: 12px;
  background-size: cover;
  background-position: center;
  image-rendering: crisp-edges;
  image-rendering: pixelated;
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
  grid-template-rows: repeat(auto-fill, 100px);
  grid-auto-flow: column;
  gap: 20px;
  position: relative;
  z-index: 1;
}

.OpenWindowsWrapper {
  z-index: 2;
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
  position: fixed;
  width: 100px;
  height: 100px;
}
</style>
