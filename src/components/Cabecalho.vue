<script setup>
import { ref } from 'vue';
import { useDark, useToggle } from '@vueuse/core';

const isDark = useDark({
  selector: "body",
  attribute: "color-scheme",
  valueDark: "dark",
  valueLight: "light",
});
const toggle = useToggle(isDark)

const onSubmit = () => {
  toggle()
}
</script>

<template>
  <label class="switch-container">
    <input type="checkbox" @click="onSubmit">
    <span class="slider"></span>
  </label>
</template>

<style scoped>
/* The switch - the box around the slider */
.switch-container {
  position: relative;
  display: inline-block;
  width: 2.5em;
  height: 1.5em;
}

/* Hide default HTML checkbox */
.switch-container input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.switch-container .slider {
  --background: linear-gradient(to right, #090613ef, #18151f);
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--background);
  transition: background-color 0.5s;
  border-radius: 30px;
}

.switch-container .slider:before {
  position: absolute;
  content: "";
  height: 1em;
  width: 1em;
  border-radius: 50%;
  left: 10%;
  bottom: 15%;
  box-shadow: inset 15px -4px 0px 15px #f8ea27;
  background: var(--background);
  transition: transform 0.5s, box-shadow 0.5s;
}

.switch-container input:checked+.slider {
  background-color: #000;
}

.switch-container input:checked+.slider:before {
  transform: translateX(100%);
  box-shadow: inset 8px -4px 0px 0px #f8f8f4;
}
</style>