<template>
  <section class="container">
    <div class="top-container">
      <div class="score-board">
        <div class="">
          <span>{{ playerXScore }}</span>
          Player X
        </div>
        <hr />
        <div class="">
          <span>{{ playerOScore }}</span>
          Player O
        </div>
      </div>
      <h4>Active User : {{ activeUser }}</h4>
      <div v-if="gameIsOver">
        <h2>{{ message }}</h2>
        <h3>Game is Over</h3>
      </div>
    </div>
    <div class="game">
      <div
        :class="{ gameOver: gameIsOver }"
        :key="i"
        v-for="(area, i) in gameBoard"
        @click="handlePlay(i)"
        class="area"
      >
        {{ area }}
      </div>
    </div>
    <button @click="refresh()">
      <img src="../assets/refresh-icon.png" alt="" />
    </button>
  </section>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      gameIsOver: false,
      activeUser: "X",
      gameBoard: ["", "", "", "", "", "", "", "", ""],
      winningCombinations: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ],
      message: "",
      playerOScore: 0,
      playerXScore: 0,
    };
  },
  methods: {
    handlePlay(index) {
      if (!this.gameIsOver)
        if (this.gameBoard[index] === "") {
          this.gameBoard[index] = this.activeUser;
          this.checkforWin();
          this.changeUser();
        }
    },
    checkforWin() {
      for (let i = 0; i < this.winningCombinations.length; i++) {
        const [a, b, c] = this.winningCombinations[i];
        if (
          this.gameBoard[a] &&
          this.gameBoard[a] === this.gameBoard[b] &&
          this.gameBoard[b] === this.gameBoard[c]
        ) {
          this.displayWinner();
          this.changeUser();

          return;
        }
      }
      !this.gameBoard.includes("") ? this.displayTie() : undefined;
    },
    changeUser() {
      this.activeUser = this.activeUser === "X" ? "O" : "X";
    },
    displayWinner() {
      this.gameIsOver = true;
      this.activeUser == "X" ? this.playerXScore++ : this.playerOScore++;
      this.message = this.activeUser + " Wins the game";
    },
    displayTie() {
      this.gameIsOver = true;
      this.message = "It is a tie!";
    },

    refresh() {
      this.gameBoard = ["", "", "", "", "", "", "", "", ""];
      this.activeUser = "X";
      this.gameIsOver = false;
    },
  },
};
</script>

<style scoped>
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
