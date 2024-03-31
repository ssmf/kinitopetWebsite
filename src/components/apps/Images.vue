<script setup>
import { ref } from 'vue'

const imagePaths = Object.keys(import.meta.glob('/public/Media/Images/*'))

const currentImg = ref(imagePaths[0])
</script>

<template>
  <div class="Images col">
    <div class="MainWrapper row">
      <div class="ImageListWrapper col">
        <h2>C:\Pictures\</h2>
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
        <img class="ImageDisplay" :src="currentImg" />
        <div class="ButtonWrapper row">
          <button><</button>
          <button>></button>
        </div>
      </div>
    </div>
    <div class="ImageDetails"></div>
  </div>
</template>

<style scoped>
h2 {
  font-size: var(--windowSecondHeaderSize);
  text-align: center;
}

p {
  font-size: var(--windowTextSize);
}

.Images {
  align-items: stretch;
  width: 900px;
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
  flex: 4;
}

.ImageDisplay {
  height: 100%;
  width: 100%;
}

.ImageDetails {
  height: 80px;
}

.ImageName {
  cursor: pointer;
}

.ImageName:hover {
  color: var(--gray);
}

.Selected {
  background-color: var(--darkBlue);
  color: white;
}
</style>
