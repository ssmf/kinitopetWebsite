<script setup>
import { ref } from 'vue'

const inputElement = ref(null)

const inputValue = ref('')

const clearTerminal = () => {
  console.log('clear')
}

const currentOutputs = ref([
  'KinitoOS 1993 - 1999',
  'Use "help" command to get list of all commands avaialble!'
])

const commandList = [
  { command: 'help', func: clearTerminal },
  { command: 'resetDesktop', func: clearTerminal },
  { command: 'resetPersonalization', func: clearTerminal },
  { command: 'reboot', func: clearTerminal },
  { command: 'shutDown', func: clearTerminal },
  { command: 'aboutCreator', func: clearTerminal },
  { command: 'close', func: clearTerminal },
  { command: 'clear', func: clearTerminal }
]

const enterValue = () => {
  const cmnd = commandList.find((e) => e.command == inputValue.value)
  cmnd ? cmnd.func() : (inputValue.value = '')
}

const throwError = (err) => {}
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
