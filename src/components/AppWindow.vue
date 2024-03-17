<script setup>
import { useElementSize, useMouse } from '@vueuse/core'
import { defineAsyncComponent, onMounted, ref } from 'vue'

const props = defineProps(['Name', 'IconExtension', 'MousePos'])
const windowDom = ref(null)
const mousePos = ref(useMouse())

const WindowContent = defineAsyncComponent(
  () => import(`./apps/${props.Name.split(' ').join('')}.vue`)
)
const appIcon = new URL(
  '/Assets/Media/' + props.Name.split(' ').join('') + '.' + props.IconExtension,
  import.meta.url
).href

onMounted(() => {
  windowDom.value.style.top = props.MousePos.y + 'px'
  windowDom.value.style.left = props.MousePos.x + 'px'
})

const isDragging = ref(false)
const windowSize = ref(null)

const startDragging = () => {
  windowSize.value = useElementSize(windowDom)
  isDragging.value = true
  console.log('started dragging!')
}

const stopDragging = () => {
  isDragging.value = false
  console.log('stopped dragging!')
}
</script>

<template>
  <div
    class="Window"
    ref="windowDom"
    :style="
      isDragging
        ? { top: mousePos.y - 10 + 'px', left: mousePos.x - windowSize.width / 2 + 'px' }
        : { top: mousePos.y, left: mousePos.y }
    "
  >
    <div class="TopBar" @mousedown="startDragging" @mouseup="stopDragging">
      <div class="AppDetails">
        <img :src="appIcon" alt="icon of the app" class="AppIcon" />
        <p class="AppName">{{ Name }}</p>
      </div>
      <div class="Options"></div>
    </div>
    <div class="Content">
      <WindowContent></WindowContent>
    </div>
  </div>
</template>

<style scoped>
.Window {
  position: fixed;
  width: fit-content;
  border: 10px solid var(--gray);
  background-color: var(--gray);
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.TopBar {
  background-color: var(--darkGray);
  height: 30px;
  padding: 3px 6px;
  display: flex;
  justify-content: space-between;
}

.AppDetails {
  display: flex;
  gap: 5px;
  color: white;
  text-shadow: 2px 2px 0px black;
  user-select: none;
}

.AppIcon {
  height: 100%;
}

.Content {
  padding: 10px;
  border: 2px solid (--darkGray);
  background-color: white;
}
</style>
