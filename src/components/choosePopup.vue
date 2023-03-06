import { emit } from 'process';

<template>
  <div class="choose-popup">
    <h3 class="header">{{ header }}</h3>
    <div class="button-container">
      <button
        class="choose-button"
        :class="{ 'no-image': !firstImage }"
        @click="$emit('choose', 'first')"
      >
        <span>{{ firstValue }}</span>
        <img
          v-if="firstImage"
          :src="require(`../assets/${firstImage}`)"
          alt=""
        />
      </button>

      <button
        class="choose-button"
        :class="{ 'no-image': !secondImage }"
        @click="$emit('choose', 'second')"
      >
        <span>{{ secondValue }}</span>
        <img
          v-if="secondImage"
          :src="require(`../assets/${secondImage}`)"
          alt=""
        />
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: ["firstValue", "secondValue", "header", "firstImage", "secondImage"],
};
</script>
<style scoped>
.choose-popup {
  background-color: white;
  position: absolute;
  text-align: center;
  z-index: 10;
  top: 10vh;
  padding: 2rem;
  border-radius: 20px;
}
.choose-button {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 4rem;
  font-size: x-large;
  padding: 0 0 3rem 0;
  background-color: #95e9ff;
  color: white;
  border-radius: 20px;
  position: relative;
  border-bottom: 6px solid #3ecefe;
  width: 40%;
}
.choose-popup span {
  font-weight: bold;
  width: 100%;
  background-color: #3ecefe;
  padding: 1rem;
  border-radius: 20px 20px 0 0;
}

.button-container {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.choose-popup h3 {
  font-size: xx-large;

  padding: 2px 50px;
  background-color: #a77dfe;
  border-radius: 20px;
  color: white;
  margin: auto;
  margin-bottom: 2rem;
  border-radius: 20px;
}
.no-image {
  padding: 0;
  border: none;
}
.no-image span {
  border-radius: 30px;
}

@media only screen and (max-width: 950px) {
  .choose-popup button span {
    font-size: 16px;
  }
  .choose-popup {
    width: min-content;
  }
  .choose-popup h3 {
    font-size: 20px;
  }
}
@media only screen and (max-width: 500px) {
  .choose-popup {
    width: 90vw;
    padding: 0.5rem;
  }

  .choose-popup h3 {
    font-size: 18px;
  }
}
</style>
