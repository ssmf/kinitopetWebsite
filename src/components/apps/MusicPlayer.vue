<script setup>
import { ref } from 'vue'

const aud = new Audio(new URL('/Music/Bliss.mp3', import.meta.url).href)

aud.play()

const loop = ref(false)
const autoPlay = ref(false)
const on = ref(true)
const sync = ref(false)

const songs = new URL('/Music/a world I build for you [KinitoPET OST].mp3', import.meta.url).href

console.log(songs)
console.log('test')
</script>

<template>
  <div class="MusicPlayer">
    <div class="Main col">
      <div class="Visualizer"></div>
      <div class="TimeLine"></div>
      <div class="Wrapper row">
        <div class="Interactions col">
          <h4 style="font-size: var(--windowTextSize)">00:46 / 2:32</h4>
          <div class="Buttons SongButtons row">
            <img class="Button SongButton" src="/public/Media/PreviousSong.webp" />
            <img class="Button SongButton" src="/public/Media/PlaySong.webp" />
            <img class="Button SongButton" src="/public/Media/PauseSong.webp" />
            <img class="Button SongButton" src="/public/Media/StopSong.webp" />
            <img class="Button SongButton" src="/public/Media/SkipSong.webp" />
          </div>
          <h5 style="font-size: calc(var(--windowTextSize) - 5px)">44KHz 192KBps</h5>
        </div>
        <div class="Buttons row">
          <button class="Button" @click="loop = !loop" :class="{ ButtonPressed: loop }">
            LOOP
          </button>
          <button class="Button" @click="autoPlay = !autoPlay" :class="{ ButtonPressed: autoPlay }">
            AUTO
          </button>
          <button class="Button" @click="on = !on" :class="{ ButtonPressed: on }">ON</button>
          <button class="Button" @click="sync = !sync" :class="{ ButtonPressed: sync }">
            SYNC
          </button>
        </div>
        <img class="Logo" src="/Media/KinitoOS.png" />
        <div class="Sliders row">
          <div class="SliderWrapper col">
            <input min="0" max="100" step="5" type="range" class="Slider" orient="vertical" />
            <h5 class="SliderText">Vol</h5>
          </div>
          <div class="SliderWrapper col">
            <input min="0" max="100" step="5" type="range" class="Slider" orient="vertical" />
            <h5 class="SliderText">L/R</h5>
          </div>
          <div class="SliderWrapper col">
            <input min="0" max="100" step="5" type="range" class="Slider" orient="vertical" />
            <h5 class="SliderText">Bass</h5>
          </div>
        </div>
      </div>
    </div>
    <div class="TracListWrapper col">
      <h2 class="TrackListHeading">KinitoPET OST</h2>
      <div class="TrackList">
        <div class="Track"><p class="TrackName">1. My new friend [KinitoPET OST]</p></div>
        <div class="Track"><p class="TrackName">1. My new friend [KinitoPET OST]</p></div>
        <div class="Track"><p class="TrackName">1. My new friend [KinitoPET OST]</p></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.row {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.col {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex-wrap: wrap;
}

.MusicPlayer {
  display: flex;
}
.Main {
}

.Visualizer {
  width: 100%;
  height: 200px;
}

.Wrapper {
  gap: 10px;
}

.Buttons {
  width: 130px;
  gap: 10px;
  justify-content: center;
  box-sizing: border-box;
}

.SongButtons {
  width: 100%;
}

.Button {
  font: var(--smallButtonFontSize);
  border-radius: 0;
  background-color: var(--lightGray);
  border-bottom: 1px solid black;
  border-right: 1px solid black;
  width: 60px;
}

.SongButton {
  width: 40px;
}

.Button:hover {
  cursor: pointer;
}

.ButtonPressed {
  background-color: var(--gray);
  border: 1px solid black;
  border-left: 2px solid black;
  border-top: 2px solid black;
  position: relative;
  top: 3px;
  left: 1px;
}

.Sliders {
  gap: 10px;
}

.SliderWrapper {
  height: 200px;
}

.Slider {
}

input[type='range']::-webkit-slider-thumb,
input[type='range']::-moz-range-thumb {
  border-radius: 0px;
  height: 10px;
  width: 20px;
  background-color: var(--lightGray);
  border: 1px solid black;
  cursor: pointer;
}

input[type='range']::-moz-range-track,
input[type='range']::-webkit-slider-runnable-track {
  width: 4px;
  height: 100%;
  background: var(--gray);
  border: 0px;
  border-bottom: 1.3px solid black;
  border-right: 1.3px solid black;
  cursor: pointer;
}

.TracListWrapper {
  gap: 20px;
}

.TrackList {
  border: 2px solid black;
  border-bottom: 1px solid black;
}

@keyframes moveTrackTitle {
  from {
    margin-left: 0;
  }
  5% {
    margin-left: 0;
  }
  90% {
    margin-left: -100%;
  }
  to {
    margin-left: -100%;
  }
}

.Track {
  border-bottom: 1px solid black;
  padding: 8px;
  font-size: var(--windowSecondHeaderSize);
  width: 200px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  text-wrap: nowrap;
  overflow: hidden;
}

.Track:hover {
  cursor: pointer;
  background-color: var(--lightGray);
}

.TrackName {
  animation: 5s infinite moveTrackTitle;
  animation-timing-function: steps(30, end);
  user-select: none;
}

.TrackListHeading {
  font-size: var(--windowSecondHeaderSize);
  text-align: center;
  background-color: var(--pink);
  border-radius: 5px;
  width: 100%;
}
</style>
