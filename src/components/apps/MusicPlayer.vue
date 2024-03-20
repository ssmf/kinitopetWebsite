<script setup></script>

<template>
  <div class="MusicPlayer">
    <div class="Main col">
      <div class="Visualizer"></div>
      <div class="TimeLine"></div>
      <div class="Wrapper row">
        <div class="Interactions">
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
            <input type="range" class="Slider" orient="vertical" />
            <h5 class="SliderText">Vol</h5>
          </div>
          <div class="SliderWrapper col">
            <input type="range" class="Slider" orient="vertical" />
            <h5 class="SliderText">L/R</h5>
          </div>
          <div class="SliderWrapper col">
            <input type="range" class="Slider" orient="vertical" />
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
  width: 100px;
  gap: 10px;
  justify-content: center;
}

.Button {
  width: 45px;
}

.Sliders {
  gap: 10px;
}

.SliderWrapper {
  height: 200px;
}

.Slider {
}

.TrackListHeading {
  text-align: center;
}
</style>
