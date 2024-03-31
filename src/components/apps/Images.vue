<script setup>
import { ref, watch } from 'vue'

const imagePaths = Object.keys(import.meta.glob('/public/Media/Images/*'))

const currentImg = ref(imagePaths[0])

const skipImg = (val) => {
  currentImg.value =
    imagePaths[
      Math.min(Math.max(0, imagePaths.indexOf(currentImg.value) + val), imagePaths.length - 1)
    ]
}

const imageName = ref(
  `Name: ${currentImg.value.replace('/public/Media/Images/', '').replace('.webp', '')}`
)
const imageTime = ref(`Time: ${12 + Math.floor(Math.random() * (30 - 12))} years ago`)
const imageSize = ref(`Size: ${5 + Math.floor(Math.random() * (40 - 5))}Kb`)
const imagePath = ref(
  `Path: C:\\Media\\Pictures\\${currentImg.value.replace('/public/Media/Images/', '')}`
)

const generateImageDetails = () => {
  imageName.value = `Name: ${currentImg.value.replace('/public/Media/Images/', '').replace('.webp', '')}`
  imageTime.value = `Time: ${12 + Math.floor(Math.random() * (30 - 12))} years ago`
  imageSize.value = `Size: ${5 + Math.floor(Math.random() * (40 - 5))}Kb`
  imagePath.value = `Path: C:\\Media\\Pictures\\${currentImg.value.replace('/public/Media/Images/', '')}`
}

watch(currentImg, generateImageDetails)

const getSRC = (src) => {
  return new URL(src.replace('/public', ''), import.meta.url).href
}
</script>

<template>
  <div class="Images col">
    <div class="MainWrapper row">
      <div class="ImageListWrapper col">
        <h2>C:\Media\Pictures\</h2>
        <div class="ImageList col">
          <p
            v-for="imgPath in imagePaths"
            :key="JSON.stringify(imgPath)"
            @click="currentImg = imgPath"
            :class="{ Selected: currentImg == imgPath }"
            class="ImageName"
          >
            {{ imgPath.replace('/public/Media/Images/', '') }}
          </p>
        </div>
      </div>
      <div class="col ImageWrapper">
        <img class="ImageDisplay" :src="getSRC(currentImg)" />
        <div class="ButtonWrapper row">
          <button @click="skipImg(-1)"><</button>
          <button @click="skipImg(1)">></button>
        </div>
      </div>
    </div>
    <div class="ImageDetails col">
      <p>{{ imageName }}</p>
      <p>{{ imageTime }}</p>
      <p>{{ imageSize }}</p>
      <p>{{ imagePath }}</p>
    </div>
  </div>
</template>

<style scoped>
.Images {
  align-items: stretch;
  width: 1000px;
}

h2 {
  font-size: var(--windowSecondHeaderSize);
  text-align: center;
}

p {
  font-size: var(--windowTextSize);
}

.ButtonWrapper {
  justify-content: space-between;
  width: 100%;
  padding: 2px 30px;
}

button {
  font-size: var(--smallButtonFontSize);
  padding: 5px 10px;
  background-color: var(--gray);
  border: 1px solid var(--lightGray);
  box-shadow: 1px 1px 0px 1px black;
  cursor: pointer;
  position: relative;
}

button:active {
  top: 2px;
  left: 2px;
  box-shadow: -1px -1px 0px 1px black;
}

.MainWrapper {
  height: 550px;
  align-items: stretch;
  gap: 20px;
  padding: 5px;
}

.ImageListWrapper {
  flex: 1;
  justify-content: flex-start;
  align-items: stretch;
  padding: 3px;
  border: 3px solid black;
  box-shadow: 2px 2px 0px 2px var(--darkGray);
}

.ImageList {
  align-items: flex-end;
  padding: 5px;
}

.ImageWrapper {
  flex: 3;
  gap: 5px;
}

.ImageDisplay {
  height: 500px;
  width: 100%;
}

.ImageName {
  cursor: pointer;
  padding: 1px 3px;
}

.ImageName:hover {
  color: var(--gray);
}

.Selected {
  background-color: var(--darkBlue);
  color: white;
}
</style>
