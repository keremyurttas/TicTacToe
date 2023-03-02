import { emit } from 'process';

<template>
  <div class="choose-popup">
    <h3>{{ header }}</h3>
    <div class="button-container">
      <button @click="$emit('choose', 'first')">{{ firstValue }}</button>

      <button @click="$emit('choose', 'second')">
        {{ secondValue }}
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: ["firstValue", "secondValue", "header"],
};
</script>
<style scoped>
.choose-popup {
  width: 50vw;
  background-color: rgb(118, 117, 118);

  position: absolute;
  text-align: center;
  z-index: 10;
  top: 5vh;
  padding: 2rem;
  border-radius: 20px;
}
.choose-popup button {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: x-large;
  padding: 1rem 2rem;
  background-color: blueviolet;
  color: white;
  border-radius: 10px;
}
.choose-popup button:hover {
  transform: scale(1.1);
}
.choose-popup hr {
  width: 2px;
  height: 100%;
}
.button-container {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.choose-popup h3 {
  font-size: xx-large;
  margin-bottom: 2rem;
}
@media only screen and (max-width: 950px) {
  .choose-popup button {
    font-size: 18px;
  }
  .choose-popup {
    width: 70vw;
  }
}
@media only screen and (max-width: 500px) {
  .choose-popup {
    width: 90vw;
  }
  .choose-popup button {
    padding: 1rem;
  }
  .choose-popup h3 {
    font-size: 24px;
  }
}
</style>
