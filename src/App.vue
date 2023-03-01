<template>
  <div class="container">
    <h1 class="header">Tic Tac Toe</h1>

    <choose-popup
      v-if="gameType == null"
      @choose="gameType = $event == 'first' ? 'singlePlayer' : 'multiPlayer'"
      header="How do you want to play?"
      firstValue="Single player"
      secondValue="Multi Player"
    ></choose-popup>
    <component v-if="gameType != null" :is="gameType"></component>
    <button class="return" @click="gameType = null" v-if="gameType !== null">
      Return to menu
    </button>
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
/* reset.css */
body * {
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}
button {
  background-color: transparent;
  border: none;
  cursor: pointer;
}
h4,
h2,
h3,
h6,
h1 {
  margin: 0;
}

/* stylings */
.header {
  width: max-content;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 20px;
  position: relative;
}
.game {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 5px;
  position: relative;
}

.board-cell {
  border: 2px solid #000;
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 4rem;
  font-weight: 600;
  cursor: pointer;
  background-color: #c9f9fc;
  border-radius: 5px;
  color: #fbb500;
}

.score-board {
  position: relative;
  display: flex;
  justify-content: space-between;
  height: max-content;
  font-weight: 500;
  color: white;
}
.score-board strong {
  display: block;
  font-size: larger;
  color: black;
}
.activeUser {
  color: blueviolet;
}

.top-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 10px;
  background-color: #fcd015;
  padding: 1rem;
  border-radius: 10px;
}
.gameOver {
  background-color: #648083;
}
.return {
  background-color: #648083;
  color: white;
  padding: 1rem 2rem;
  border-radius: 8px;
}
</style>
