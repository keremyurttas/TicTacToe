<template>
  <section class="container">
    <choose-popup
      @choose="userChoice = $event == 'first' ? 'X' : 'O'"
      v-if="userChoice == ''"
      firstValue="X"
      secondValue="O"
    ></choose-popup>
    <div class="top-container">
      <div class="score-board">
        <div class="">
          <span>{{ playerScore }}</span>
          You
        </div>
        <hr />
        <div class="">
          <span>{{ computerScore }}</span>
          Computer
        </div>
      </div>
      <div class="status-container">
        <h4>Your turn</h4>
        <h6>Choosed {{ userChoice }}</h6>
      </div>
      <div v-if="gameIsOver">
        <h2>{{ message }}</h2>
        <h3>Game is Over</h3>
      </div>
    </div>
    <div class="game">
      <div
        :class="{ gameOver: gameIsOver || timeoutActive }"
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
import choosePopup from "./choosePopup.vue";
export default {
  name: "App",
  components: { choosePopup },

  data() {
    return {
      gameIsOver: false,
      timeoutActive: false,
      userChoice: "",
      computerChoice: "",
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
      playerScore: 0,
      computerScore: 0,
    };
  },
  methods: {
    handlePlay(index) {
      if (!this.gameIsOver && !this.timeoutActive)
        if (this.gameBoard[index] === "") {
          this.gameBoard[index] = this.userChoice;
          this.checkforWin();
          this.timeoutActive = true;
          setTimeout(() => {
            this.computerPlay();
            this.timeoutActive = false;
          }, 500);
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
          console.log(this.computerChoice);
          const winner =
            this.gameBoard[a] === this.computerChoice ? "Computer" : "You";
          this.displayWinner(winner);

          return;
        }
      }
      !this.gameBoard.includes("") ? this.displayTie() : undefined;
    },
    computerPlay() {
      if (!this.gameIsOver) {
        let emptySquares = [];
        this.gameBoard.filter((square, i) =>
          square == "" ? emptySquares.push(i) : undefined
        );
        let randomIndex =
          emptySquares[Math.floor(Math.random() * emptySquares.length)];
        this.gameBoard[randomIndex] = this.computerChoice;
        this.checkforWin();
      }
    },
    displayWinner(winner) {
      this.gameIsOver = true;
      this.message = winner + " Win the game";
      winner == "You" ? this.playerScore++ : this.computerScore++;
    },
    displayTie() {
      this.gameIsOver = true;
      this.message = "It is a tie!";
    },

    refresh() {
      this.gameBoard = ["", "", "", "", "", "", "", "", ""];
      this.gameIsOver = false;
      this.userChoice = "";
    },
  },

  watch: {
    userChoice() {
      this.computerChoice = this.userChoice === "X" ? "O" : "X";
    },
  },
};
</script>

<style scoped>
.status-container {
  display: flex;
  justify-content: space-between;
  height: max-content;
  align-items: center;
}
</style>
