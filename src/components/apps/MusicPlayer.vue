<script setup>
import { ref, onMounted } from 'vue'

const loop = ref(false)
const autoPlay = ref(false)
const on = ref(true)
const sync = ref(false)

const songsDom = ref(null)
const TracksDom = ref(null)

let currentSong = null

const songsPaths = Object.keys(import.meta.glob('/public/Music/*'))
const songs = ref([])

onMounted(() => {
  songsPaths.forEach((song) => {
    const renderedSong = new Audio(song)
    songsDom.value.appendChild(renderedSong)
    songs.value.push(renderedSong)
  })
  currentSong = songs.value[0]
  songs.value[0].play()

  TracksDom.value.forEach((e) => {
    const currentPar = e.querySelector('p')
    currentPar.style['animation-duration'] =
      `${Math.floor((currentPar.offsetWidth / 50) * 10) / 10}s`
  })
})

const PlayNewSong = (newSong) => {
  currentSong.pause()
  currentSong = newSong
  currentSong.play()
}
</script>

<template>
  <div class="MusicPlayer">
    <div class="songs" ref="songsDom"></div>
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
    <div class="TrackListWrapper col" style="flex-wrap: nowrap">
      <h2 class="TrackListHeading">KinitoPET OST</h2>
      <div class="TrackList">
        <div
          v-for="song in songsPaths"
          @click="PlayNewSong(songs.find((e) => e.getAttribute('src') == song))"
          :key="song"
          class="Track"
          ref="TracksDom"
        >
          <p :id="song + 'Title'" class="TrackName">
            {{ song.replace('/public/Music/', '') }}
          </p>
        </div>
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
  height: 500px;
  width: max-content;
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

.TrackListWrapper {
  height: 100%;
  gap: 20px;
}

.TrackList {
  padding-right: 5px;
  border: 2px solid black;
  border-bottom: 1px solid black;
  overflow-x: hidden;
  overflow-y: auto;
}

@keyframes moveTrackTitle {
  from {
    transform: translateX(0%);
  }
  5% {
    transform: translateX(0%);
  }
  90% {
    transform: translateX(min(calc(180px - 100%), 0%));
  }
  to {
    transform: translateX(min(calc(180px - 100%), 0%));
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
  position: relative;
  animation-name: moveTrackTitle;
  animation-iteration-count: infinite;
  animation-timing-function: steps(25, end);
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
