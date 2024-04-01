<script setup>
import { ref, inject } from 'vue'

const inputElement = ref(null)

const inputValue = ref('')
const ResetDesktopFiles = inject('ResetDesktopFiles')
const { changeTheme } = inject('currentTheme')
const { changeWallpaper } = inject('currentWallpaper')

const clearTerminal = () => {
  console.log('clear')
}

const resetPers = () => {
  changeTheme({ mainColor: '#807e7e', secondaryColor: '#c3c3c3' })
  changeWallpaper('/public/Media/Wallpapers/Wallpaper1.webp')
}

const resetDesktop = () => {
  ResetDesktopFiles()
}

const currentOutputs = ref([
  'KinitoOS 1993 - 1999',
  'Use "help" command to get list of all commands avaialble!'
])

const commandList = [
  { command: 'help', func: clearTerminal },
  { command: 'resetDesktop', func: resetDesktop },
  { command: 'resetPersonalization', func: resetPers },
  { command: 'reboot', func: clearTerminal },
  { command: 'shutDown', func: clearTerminal },
  { command: 'aboutCreator', func: clearTerminal },
  { command: 'close', func: clearTerminal },
  { command: 'clear', func: clearTerminal }
]

const enterValue = () => {
  const cmnd = commandList.find((e) => e.command == inputValue.value)
  cmnd ? cmnd.func() : throwError(inputValue.value)
  inputValue.value = ''
}

const throwError = (err) => {
  currentOutputs.value.push(`Command '${err}' is not recognized.`)
}
</script>

<template>
  <div class="Terminal col" @click="inputElement.focus()">
    <div class="Output">
      <p
        v-for="currentOutput in currentOutputs"
        :key="JSON.stringify(currentOutputs.indexOf(currentOutput))"
      >
        {{ currentOutput }}
      </p>
    </div>
    <div class="Wrapper row">
      <p>></p>
      <div class="InputWrapper">
        <input
          type="text"
          class="InputElement"
          ref="inputElement"
          v-model="inputValue"
          @keydown.enter="enterValue"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-size: var(--windowTextSize);
}

p {
  font-size: var(--windowSmallTextSize);
}

.Terminal {
  width: 800px;
  height: 450px;
  background-color: black;
  color: white;
  padding: 5px;
  font-size: var(--windowSmallTextSize);
  justify-content: stretch;
  align-items: stretch;
}

.Output {
  flex: 9;
}

.Wrapper {
  width: 100%;
  gap: 3px;
  flex: 1;
}

.InputWrapper {
  width: 100%;
}

::-moz-selection {
  color: black;
  background: white;
}

::selection {
  color: black;
  background: white;
}

.InputElement {
  font-size: var(--windowSmallTextSize);
  width: 100%;
  padding: 0px;
  border: 0px;
  background-color: rgba(0, 0, 0, 0);
  color: white;
  min-height: 30px;
  margin-top: 2px;
}

.InputElement:focus {
  outline: none;
}
</style>
