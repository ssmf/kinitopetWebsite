<script setup></script>

<template>
  <div class="Terminal col">
    <div class="Output"></div>
    <div class="Wrapper row">
      <p>></p>
      <div class="InputWrapper"><input type="text" class="InputElement" /></div>
    </div>
  </div>
</template>

<style scoped>
.Terminal {
  width: 800px;
  height: 450px;
  background-color: black;
  color: white;
  padding: 5px;
  font-size: var(--windowSmallTextSize);
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
}

.InputElement:focus {
  outline: none;
}
</style>
