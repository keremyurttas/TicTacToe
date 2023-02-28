import { emit } from 'process';

<template>
  <div class="choose-popup">
    <button @click="$emit('choose', 'first')">{{ firstValue }}</button>
    <hr />
    <button @click="$emit('choose', 'second')">{{ secondValue }}</button>
  </div>
</template>
<script>
export default {
  props: ["firstValue", "secondValue"],
};
</script>
<style scoped>
.choose-popup {
  width: 100%;
  height: 100%;
  backdrop-filter: blur 2px;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  z-index: 10;
}
.choose-popup button {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: dimgrey;
}
.choose-popup button:hover {
  transform: scale(1.1);
}
.choose-popup hr {
  width: 2px;
  height: 100%;
}
</style>
