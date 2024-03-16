<script setup>
import Desktop from '@/components/Desktop.vue'
import Taskbar from '@/components/Taskbar.vue'
</script>

<template>
  <div class="main">
    <Desktop></Desktop>
    <Taskbar></Taskbar>
  </div>
</template>

<style scoped>
.main {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: stretch;
}
</style>
