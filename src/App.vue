<template>
  <div class="container">
    <h1 class="header">Tic Tac Toe</h1>

    <choose-popup
      v-if="gameType == null"
      @choose="gameType = $event == 'first' ? 'singlePlayer' : 'multiPlayer'"
      header="How do you want to play?"
      firstValue="Single player"
      firstImage="icons8-battle-48.png"
      secondValue="Multi Player"
      secondImage="icons8-multiplayer-48.png"
    ></choose-popup>
    <component
      @refresh="gameType = null"
      v-if="gameType != null"
      :is="gameType"
    ></component>
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
body {
  background: radial-gradient(circle, #a659fe 0%, #6f53fd 100%);
}
button:hover {
  transform: scale(1.1);
}
.header {
  width: max-content;
  background-color: #9f51fe;
  border: 6px solid white;
  border-radius: 20px;
  padding: 4px 20px;
  color: white;
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
}

.board-cell {
  border: 3px solid white;
  width: 100px;
  aspect-ratio: 1/1;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 4rem;
  font-weight: 600;
  cursor: pointer;
  background-color: #4cdafe;
  border-radius: 16px;
  border-bottom: #08b9ff solid 6px;
  color: white;
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
  background-color: #67eb00;
  border-bottom: #4ec306 solid 6px;
  padding: 1rem;
  border-radius: 20px;
}
.top-container hr {
  background-color: white;
  width: 6px;
  border: none;
  border-radius: 30px;
}
.player-stats {
  position: relative;
}
.gameOver {
  background-color: #0896cf;
}
.return {
  background-color: #fc8aff;
  color: white;
  border: 2px solid white;
  padding: 1rem 2rem;
  border-radius: 20px;
  font-weight: 600;
  font-size: medium;
  border-bottom: #da57f0 solid 6px;
}
@keyframes lineH {
  0% {
    width: 0%;
  }
  100% {
    width: 100%;
  }
}
.player-bar {
  width: 100%;
  background: white;
  height: 5px;
  border-radius: 20px;
  margin-top: 2px;
  animation: lineH 0.2s linear;
}
@media only screen and (max-width: 950px) {
  .board-cell {
    width: 15vw;
  }
  .top-container {
    font-size: x-large;
  }
}
@media only screen and (max-width: 500px) {
  .board-cell {
    width: 20vw;
    font-size: 3rem;
  }
  .top-container {
    font-size: large;
  }
}
</style>
