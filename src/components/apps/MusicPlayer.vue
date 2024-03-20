<script setup></script>

<template>
  <div class="MusicPlayer">
    <div class="Main col">
      <div class="Visualizer"></div>
      <div class="TimeLine"></div>
      <div class="Wrapper row">
        <div class="Interactions col">
          <h4>00:46 / 2:32</h4>
          <div class="Buttons SongButtons row"></div>
          <h5>44KHz 192KBps</h5>
        </div>
        <div class="Buttons row">
          <button class="Button">LOOP</button>
          <button class="Button">AUTO</button>
          <button class="Button">ON</button>
          <button class="Button">SYNC</button>
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
    <div class="TracListWrapper">
      <h2 class="TrackListHeading">KinitoPET OST</h2>
      <div class="TrackList">
        <div class="Track">
          <p>1. My new friend [KinitoPET OST]</p>
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
}

.Button {
  font: var(--smallButtonFontSize);
  border-radius: 0;
  background-color: var(--lightGray);
  border: 0px;
  border-bottom: 1px solid black;
  border-right: 1px solid black;
  width: 60px;
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
}

input[type='range']::-moz-range-track,
input[type='range']::-webkit-slider-runnable-track {
  width: 4px;
  height: 100%;
  background: var(--gray);
  border: 0px;
  border-bottom: 1.3px solid black;
  border-right: 1.3px solid black;
}

.TrackListHeading {
  text-align: center;
}
</style>
