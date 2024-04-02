<script setup>
import { useDateFormat } from '@vueuse/core'
import { ref, onMounted, watch, computed, inject } from 'vue'
import AudioVisualizer from '@/components/AudioVisualizer.vue'

const { currentTheme } = inject('currentTheme')

const isPlaying = ref(false)
const stopped = ref(true)
const loop = ref(false)
const autoPlay = ref(false)
const on = ref(true)
const sync = ref(false)

const songsDom = ref(null)
const TracksDom = ref(null)

const volume = ref(0.5)
const LR = ref(0)
const bass = ref(0)

const audioctx = new AudioContext()

const analyzer = ref(audioctx.createAnalyser())
analyzer.value.fftSize = 128
analyzer.value.connect(audioctx.destination)

const panner = audioctx.createStereoPanner()
panner.connect(analyzer.value)

const bassFilter = audioctx.createBiquadFilter()
bassFilter.type = 'lowshelf'
bassFilter.frequency.value = 200
bassFilter.connect(panner)

watch(bass, (curr) => {
  bassFilter.gain.value = curr
})

watch(LR, (curr) => {
  panner.pan.value = curr
})

const songsPaths = Object.keys(import.meta.glob('/public/Music/*'))

let currentSong = ref({ id: '/public/Music/A world I build for you.mp3' })
const songs = ref(null)

onMounted(() => {
  currentSong.value = songs.value[0]

  TracksDom.value.forEach((e) => {
    const currentPar = e.querySelector('p')
    currentPar.style['animation-duration'] =
      `${Math.floor((currentPar.offsetWidth / 50) * 10) / 10}s`
  })

  songs.value.forEach((e) => {
    const audioSrc = audioctx.createMediaElementSource(e)
    audioSrc.connect(bassFilter)
  })

  watch(volume, (curr) => {
    songs.value.forEach((e) => {
      e.volume = curr
    })
  })
})

const PlayNewSong = (newSong) => {
  currentSong.value.pause()
  currentSong.value.currentTime = 0
  currentSong.value = newSong
  currentSong.value.play()
  isPlaying.value = true
  stopped.value = false
}

const SkipSong = (num) => {
  stopped.value = false
  currentSong.value.pause()
  currentSong.value.currentTime = 0
  const currentId = songs.value.indexOf(currentSong.value)
  let newId = currentId
  if ((num > 0 && currentId < songs.value.length - 1) || (num < 0 && currentId > 0)) {
    newId += num
  } else {
    newId = 0
  }
  currentSong.value = songs.value[newId]
  if (isPlaying.value) {
    currentSong.value.play()
  }
}

const ResetSong = () => {
  isPlaying.value = false
  stopped.value = true
  currentSong.value.pause()
  currentSong.value.currentTime = 0
  currentSong.value = songs.value[0]
}

const songEnded = () => {
  if (loop.value) {
    currentSong.value.currentTime = 0
    currentSong.value.play()
  } else if (autoPlay.value) {
    SkipSong(1)
  } else {
    isPlaying.value = false
  }
}

const getSRC = (song) => {
  return new URL(song.replace('/public', ''), import.meta.url).href
}
</script>

<template>
  <div class="AudioPlayer">
    <div class="songs" ref="songsDom">
      <audio
        @ended="songEnded"
        v-for="song in songsPaths"
        :key="JSON.stringify(song)"
        :id="song"
        :src="getSRC(song)"
        ref="songs"
      ></audio>
    </div>
    <div class="Main col" style="flex-wrap: nowrap">
      <AudioVisualizer v-model:analyzer="analyzer"></AudioVisualizer>
      <div class="SongTitle">{{ currentSong.id.replace('/public/Music/', '') }}</div>
      <div class="Wrapper row">
        <div class="Interactions col">
          <Suspense>
            <h4 style="font-size: var(--windowTextSize)">
              {{
                useDateFormat(Math.floor(currentSong.currentTime * 1000), 'mm:ss').value.replace(
                  '"',
                  ''
                )
              }}
              /
              {{
                useDateFormat(Math.floor(currentSong.duration * 1000), 'mm:ss').value.replace(
                  '"',
                  ''
                )
              }}
            </h4>
          </Suspense>
          <div class="Buttons SongButtons row">
            <img
              draggable="false"
              class="Button SongButton UnTogglableButton"
              src="/public/Media/PreviousSong.webp"
              @click="SkipSong(-1)"
            />
            <img
              @click="
                () => {
                  currentSong.pause()
                  isPlaying = false
                }
              "
              draggable="false"
              class="Button SongButton"
              :class="{ ButtonPressed: !isPlaying }"
              src="/public/Media/PauseSong.webp"
            />
            <img
              @click="
                () => {
                  currentSong.play()
                  isPlaying = true
                  stopped = false
                }
              "
              draggable="false"
              class="Button SongButton"
              :class="{ ButtonPressed: isPlaying }"
              src="/public/Media/PlaySong.webp"
            />
            <img
              @click="SkipSong(1)"
              draggable="false"
              class="Button SongButton UnTogglableButton"
              src="/public/Media/SkipSong.webp"
            />
            <img
              @click="ResetSong"
              draggable="false"
              class="Button SongButton"
              :class="{ ButtonPressed: stopped }"
              src="/public/Media/StopSong.webp"
            />
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
            <input min="0" max="1" step=".05" type="range" class="Slider" v-model="volume" />
            <h5 class="SliderText">Vol</h5>
          </div>
          <div class="SliderWrapper col">
            <input min="-1" max="1" step=".1" type="range" class="Slider" v-model="LR" />
            <h5 class="SliderText">L/R</h5>
          </div>
          <div class="SliderWrapper col">
            <input min="-50" max="50" step="5" type="range" class="Slider" v-model="bass" />
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
          @click="PlayNewSong(songs.find((e) => e.getAttribute('id') == song))"
          :key="song"
          class="Track"
          ref="TracksDom"
          :class="[song == currentSong.id ? 'SelectedTrack' : '']"
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
.SelectedTrack {
  background-color: v-bind('currentTheme.secondaryColor');
}

.row {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  justify-content: space-between;
}

.col {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  flex-wrap: wrap;
}

.AudioPlayer {
  display: flex;
  height: 430px;
  width: max-content;
  display: flex;
  gap: 20px;
  background-color: white;
  padding: 10px;
}
.Main {
  margin-bottom: -70px;
}

.SongTitle {
  margin-top: 5px;
  align-self: flex-start;
  padding: 10px;
  font-size: var(--windowThirdHeaderSize);
  border: 2px solid black;
  box-shadow: 2px 2px 0px 2px var(--gray);
  color: black;
  background-color: v-bind('currentTheme.secondaryColor');
}

.SongTitle::before {
}

.Wrapper {
  gap: 10px;
  margin-top: -60px;
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
  padding: 4px;
}

.UnTogglableButton:active {
  background-color: var(--gray);
  border: 1px solid black;
  border-left: 2px solid black;
  border-top: 2px solid black;
  position: relative;
  top: 3px;
  left: 1px;
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
  margin-left: 50px;
  margin-top: 90px;
  gap: 20px;
}

.SliderWrapper {
  height: 200px;
  margin-left: -100px;
}

.Slider {
  rotate: 270deg;
}

.SliderText {
  margin-top: 80px;
}

input[type='range'] {
  appearance: none;
  -webkit-appearance: none;
}

input[type='range']::-moz-range-thumb {
  rotate: 90deg;
  border-radius: 0px;
  height: 10px;
  width: 20px;
  background-color: var(--lightGray);
  border: 1px solid black;
  cursor: pointer;
}

input[type='range']::-webkit-slider-thumb {
  appearance: none;
  -webkit-appearance: none;
  rotate: 90deg;
  border-radius: 0px;
  height: 10px;
  width: 20px;
  background-color: var(--lightGray);
  border: 1px solid black;
  cursor: pointer;
}

input[type='range']::-moz-range-track {
  width: 100%;
  height: 4px;
  background: var(--gray);
  border: 0px;
  border-bottom: 1.3px solid black;
  border-right: 1.3px solid black;
  cursor: pointer;
}

input[type='range']::-webkit-slider-runnable-track {
  width: 100%;
  height: 4px;
  background: var(--gray);
  border: 0px;
  border-bottom: 1.3px solid black;
  border-right: 1.3px solid black;
  cursor: pointer;
}

.TrackListWrapper {
  gap: 20px;
}

.TrackList {
  padding-right: 5px;
  border: 2px solid black;
  border-bottom: 1px solid black;
  overflow-x: hidden;
  overflow-y: auto;
  scroll-snap-type: y mandatory;
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
  color: v-bind('currentTheme.mainColor');
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
  scroll-snap-align: center;
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
  background-color: v-bind('currentTheme.secondaryColor');
  border-radius: 5px;
  width: 100%;
}
</style>
