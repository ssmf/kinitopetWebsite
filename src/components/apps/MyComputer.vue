<script setup>
const props = defineProps(['ComputerSpecs'])
const SessionTime = defineModel('SessionTime')
</script>

<template>
  <div class="MyComputer">
    <p>{{ rndm }}</p>
  </div>
</template>

<style scoped>
.MyComputer {
  width: 600px;
  height: 200px;
}
</style>
