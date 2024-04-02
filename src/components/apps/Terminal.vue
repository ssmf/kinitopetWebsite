<script setup>
import { ref, inject } from 'vue'

const inputElement = ref(null)

const inputValue = ref('')
const ResetDesktopFiles = inject('ResetDesktopFiles')
const { changeTheme } = inject('currentTheme')
const { changeWallpaper } = inject('currentWallpaper')
const CloseWindowFunc = inject('closeWindow')

const printMessage = (outputMsg) => {
  currentOutputs.value.push('---------------------------------------------------')
  currentOutputs.value.push(outputMsg)
}

const printHelp = () => {
  currentOutputs.value.push('---------------------------------------------------')
  currentOutputs.value.push("Here's a list of all the commands available: ")
  commandList.forEach((e) => {
    currentOutputs.value.push(`"${e.command}" - ${e.desc}`)
  })
}

const currentOutputs = ref([
  'KinitoOS 1993 - 1999',
  'Use "help" command to get list of all commands avaialble!'
])

const commandList = [
  {
    command: 'help',
    func: printHelp,
    desc: 'Prints out all of the commands available'
  },
  {
    command: 'resetDesktop',
    func: () => {
      printMessage('Desktop has been reset!')
      ResetDesktopFiles()
    },
    desc: 'Puts all of the desktop icons onto their original positions'
  },
  {
    command: 'resetPersonalization',
    func: () => {
      printMessage('Personalization has been reset!')
      changeTheme({ mainColor: '#807e7e', secondaryColor: '#c3c3c3' })
      changeWallpaper('/public/Media/Wallpapers/Wallpaper1.webp')
    },
    desc: 'Sets your theme and desktop to the default ones'
  },
  {
    command: 'reboot',
    func: () => location.reload(),
    desc: 'reboots your currently active session'
  },
  {
    command: 'shutDown',
    func: () => {
      window.close()
    },
    desc: 'deactivates your current active session'
  },
  {
    command: 'close',
    func: () => {
      CloseWindowFunc('Terminal')
    },
    desc: 'Closes the terminal window'
  },
  {
    command: 'closeAll',
    func: () => {
      CloseWindowFunc('all')
    },
    desc: 'Closes all currently active windows'
  },
  {
    command: 'clear',
    func: () => {
      currentOutputs.value = []
    },
    desc: 'Clears all of the terminal outputs'
  }
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
