<template>
  <div class="container">
    <h1>Tic Tac Toe</h1>
    <choose-popup
      v-if="gameType == null"
      @choose="gameType = $event == 'first' ? 'singlePlayer' : 'multiPlayer'"
      firstValue="Single player"
      secondValue="Multi Player"
    ></choose-popup>

    <component v-if="gameType != null" :is="gameType"></component>
  </div>
</template>
<script>
import choosePopup from "./components/choosePopup.vue";
import multiPlayer from "./components/multiPlayer.vue";
import singlePlayer from "./components/singlePlayer.vue";
export default {
  components: { singlePlayer, multiPlayer, choosePopup },
  data() {
    return {
      gameType: null,
    };
  },
};
</script>
<style>
body * {
  box-sizing: border-box;
}
button {
  background-color: transparent;
  border: none;
  cursor: pointer;
}
h4,
h2,
h3,
h6 {
  margin: 0;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 20px;
  position: relative;
  width: min-content;
  margin: auto;
}
.game {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
.gameOver {
  background-color: rgb(164, 162, 162);
}
.area {
  border: 1px solid #000;
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: xx-large;
  font-weight: 600;
  cursor: pointer;
}
.score-board span {
  display: block;
}
.score-board {
  position: relative;
  display: flex;
  justify-content: space-between;
  height: max-content;
}

.top-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
