<script setup>
import { ref } from 'vue'
const Colors = ref([
  '#000000',
  '#ffffff',
  '#7d7d7d',
  '#bcbcbc',
  '#810000',
  '#fc0000',
  '#7a7d00',
  '#fffc06',
  '#037900',
  '#01fe05',
  '#037a78',
  '#0bfaff',
  '#00057a',
  '#0601fd',
  '#7c0080',
  '#fd00f7',
  '#7d7c3c',
  '#faff7b',
  '#03353e',
  '#00ff7b',
  '#017cfd',
  '#7dfdfc',
  '#093a7d',
  '#7a7ff5',
  '#3702fe',
  '#ff007c',
  '#783903',
  '#ff7741'
])
</script>

<template>
  <div class="Paint col">
    <div class="Wrapper row">
      <div class="Tools row">
        <img class="Pen ToolbarIcon" src="/public/Media/Clover.gif" />
        <img class="Line ToolbarIcon" src="/public/Media/Clover.gif" />
        <img class="Square ToolbarIcon" src="/public/Media/Clover.gif" />
        <img class="Circle ToolbarIcon" src="/public/Media/Clover.gif" />
      </div>
      <canvas class="PaintCanvas"></canvas>
    </div>
    <div class="Colors">
      <div
        v-for="clr in Colors"
        :key="JSON.stringify(clr)"
        class="Color"
        :style="{ backgroundColor: clr }"
      ></div>
    </div>
  </div>
</template>

<style scoped>
.Wrapper {
  width: 100%;
  height: 85%;
  justify-content: stretch;
  align-items: flex-start;
  gap: 5px;
  padding: 0px 10px 10px 0px;
}

.PaintCanvas {
  width: auto;
  align-self: stretch;
  border: 5px solid black;
  box-shadow: 2px 2px 0px 2px var(--darkGray);
}

.Tools {
  padding: 5px;
  width: 100px;
  flex-wrap: wrap;
  gap: 5px;
}

.ToolbarIcon {
  position: relative;
  width: 40px;
  flex: 1;
  cursor: pointer;
}

.Paint {
  width: 900px;
  height: 600px;
  gap: 10px;
}

.Colors {
  height: min-content;
  width: min-content;
  padding: 7px;
  display: grid;
  grid-template-rows: min-content min-content;
  grid-auto-columns: min-content;
  gap: 10px;
  grid-auto-flow: column;
  background-color: var(--gray);
  align-self: flex-start;
  box-shadow: 0px 0px 0px 3px var(--darkGray);
}

.Color {
  width: 26px;
  height: 26px;
  border-top: 3px solid black;
  border-left: 3px solid black;
  cursor: pointer;
  position: relative;
}

.Color:active,
.ToolbarIcon:active {
  top: 3px;
  left: 2px;
}
</style>
