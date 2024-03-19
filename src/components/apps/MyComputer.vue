<script setup>
import { ref } from 'vue'
const props = defineProps(['ComputerSpecs'])
const SessionTime = defineModel('SessionTime')

const SpecsToDisplay = ref({ DeviceName: props.ComputerSpecs.DeviceName })

for (const spec in SpecsToDisplay.value) {
  console.log(spec)
}
</script>

<template>
  <div class="MyComputer">
    <div class="MainInfo">
      <div class="col">
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
        <div class="Spec" v-for="spec in SpecsToDisplay" :key="spec">
          <span class="gray">{{ spec }}: </span>
          <p>{{ ComputerSpecs.spec }}</p>
        </div>
      </div>
    </div>
    <div class="lineBreak"></div>
    <div class="Specifications">
      <h3>Specifications:</h3>
      <div class="col Specs"></div>
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
