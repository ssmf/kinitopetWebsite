<script setup>
import { onClickOutside } from '@vueuse/core'
import { onMounted, ref } from 'vue'

const props = defineProps(['IconPath', 'Name', 'iconScale'])

const imagePath = new URL(
  '/kinitopetWebsite/Media/' + props.IconPath.split(' ').join(''),
  import.meta.url
).href
const Select = defineModel('selectFunction')
const UnSelect = defineModel('UnSelect')

const FileDom = ref(null)

onMounted(() => {
  onClickOutside(FileDom, () => {
    UnSelect.value(props.Name)
  })
})
</script>

<template>
  <div class="File" @mousedown="Select(FileDom)" ref="FileDom">
    <img
      v-if="IconPath[IconPath.length - 1] == 'p' || IconPath[IconPath.length - 1] == 'f'"
      draggable="false"
      :src="imagePath"
      class="FileImage"
      :style="`scale: ${iconScale};`"
    />
    <video
      autoplay
      loop
      muted
      v-else
      draggable="false"
      :src="imagePath"
      class="FileImage"
      :style="`scale: ${iconScale};`"
    ></video>
    <p class="FileName">{{ Name }}</p>
  </div>
</template>

<style scoped>
.File {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  gap: 5px;
}

.FileImage {
  flex: 4;
  width: 80%;
}

.FileName {
  user-select: none;
  flex: 1;
  font-size: var(--fileNameSize);
  color: white;
  text-shadow: 2px 2px 0px black;
  position: relative;
  text-align: center;
  line-height: 100%;
}

.Overlay {
  width: 100%;
  height: 100%;
  background-color: blue;
  opacity: 0.8;
  z-index: 2;
  mix-blend-mode: multiply;
}
</style>
