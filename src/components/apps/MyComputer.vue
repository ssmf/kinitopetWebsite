<script setup>
import { ref } from 'vue'
const props = defineProps(['ComputerSpecs'])
const SessionTime = defineModel('SessionTime')

const Capacity = ref(props.ComputerSpecs.DiskSpace)
const Used = ref(Math.floor(props.ComputerSpecs.DiskSpaceTaken * 100) / 100)
const Free = ref(Math.floor((Capacity.value - Used.value) * 100) / 100)

const formatSeconds = (s) =>
  [parseInt(s / 60 / 60), parseInt((s / 60) % 60), parseInt(s % 60)]
    .join(':')
    .replace(/\b(\d)\b/g, '0$1')

const SpecsToDisplay = ref({
  'Device Name': props.ComputerSpecs.DeviceName,
  CPU: props.ComputerSpecs.CPU,
  RAM: props.ComputerSpecs.RAM + ' MB',
  'OS Type': props.ComputerSpecs.OsType,
  'OS Build': props.ComputerSpecs.OsBuild,
  'Device ID': props.ComputerSpecs.DeviceId
})
</script>

<template>
  <div class="MyComputer">
    <div class="MainInfo">
      <div class="col" :style="{ gap: '20px' }">
        <div class="col">
          <h3>Kinito OS v0.4.1</h3>
          <h4 class="pink">(pre-alpha)</h4>
        </div>
        <div class="col">
          <h3><span class="brown">All in 1</span> Bundle</h3>
          <h4>[Kinito OS + Kinito Software + Kinito Hardware]</h4>
          <h4 class="green">(active license)</h4>
        </div>
      </div>
      <img class="logo" src="/Media/KinitoOS.webp" />
    </div>
    <div class="lineBreak"></div>
    <div class="Details">
      <div class="col">
        <div class="col" :style="{ gap: '10px' }">
          <h3>Disk Space</h3>
          <div class="col Disk">
            <p>Capacity: {{ Capacity }} GB</p>
            <p>Used: {{ Used }} GB</p>
            <p>Free: {{ Free }} GB</p>
          </div>
        </div>
      </div>
      <div class="col" :style="{ gap: '7px' }">
        <h3 :style="{ rotate: '3deg', padding: '8px 0px' }">
          There is currently <span class="seaColor">{{ ComputerSpecs.FileCount }}</span> files on
          your desktop!
        </h3>
        <h3>Session time: {{ formatSeconds(SessionTime) }}</h3>
        <h3>
          Your <span class="gray">license</span> is <span class="green">valid</span> for the next
          {{ ComputerSpecs.LicenseValidationTime }} days
        </h3>
      </div>
    </div>
    <div class="lineBreak"></div>
    <div class="Specifications">
      <h3>Specifications:</h3>
      <div class="col Specs">
        <div class="Spec" v-for="(spec, name) in SpecsToDisplay" :key="name">
          <span class="gray">{{ name }}: </span> {{ spec }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.MyComputer {
  width: 800px;
  color: black;
  text-align: center;
  line-height: 32px;
  display: flex;
  flex-direction: column;
  gap: 20px;
  background-color: white;
  padding: 10px;
}

.MainInfo {
  display: flex;
  justify-content: center;
  gap: 30px;
}

.col {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0px;
}

.Specs {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 3px;
  flex-wrap: wrap;
  padding: 20px;
  height: 150px;
}

.Spec {
  font-size: var(--windowTextSize);
}

.Disk {
  line-height: 25px;
}

.Details {
  display: flex;
  justify-content: space-around;
  padding: 10px;
}

.lineBreak {
  width: 100%;
  height: 4px;
  background-color: var(--gray);
}

.logo {
  width: 60%;
}

.pink {
  color: var(--pink);
  text-shadow: 1px 1px 0px black;
}

.brown {
  color: var(--redBrown);
}

.green {
  color: var(--green);
}

.gray {
  color: var(--darkGray);
}

.seaColor {
  color: var(--seaColor);
}

h3 {
  font-size: var(--windowHeaderSize);
}

h4 {
  font-size: var(--windowSecondHeaderSize);
  color: var(--darkGray);
  padding: 0px;
}

p {
  font-size: var(--windowTextSize);
  color: var(--darkGray);
}
</style>
