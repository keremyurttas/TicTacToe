<template>
  <choose-popup
    @choose="userChoice = $event == 'first' ? 'X' : 'O'"
    v-if="userChoice == ''"
    firstValue="X"
    secondValue="O"
    header="Choose your letter !"
  ></choose-popup>
  <section v-if="userChoice" class="container">
    <div class="top-container">
      <div class="score-board">
        <div class="">
          <strong>{{ playerScore }}</strong>
          You
        </div>

        <div class="">
          <strong>{{ computerScore }}</strong>
          Computer
        </div>
      </div>
      <div v-if="!gameIsOver" class="status-container">
        <h4 :class="{ activeUser: !timeoutActive }">
          {{ !timeoutActive ? "Your turn" : "Computer Turn" }}
        </h4>
        <strong>{{ !timeoutActive ? userChoice : computerChoice }}</strong>
        <div v-if="!timeoutActive" class="player-bar"></div>
      </div>
    </div>
    <div class="game">
      <my-result
        @refresh="refresh"
        v-if="gameIsOver"
        :message="message"
      ></my-result>
      <div
        :class="{ gameOver: gameIsOver || timeoutActive }"
        :key="i"
        v-for="(area, i) in gameBoard"
        @click="handlePlay(i)"
        class="board-cell"
      >
        {{ area }}
      </div>
    </div>
    <button class="return" @click="$emit('refresh')">Return to menu</button>
  </section>
</template>

<script>
import choosePopup from "./choosePopup.vue";
import myResult from "./myResult.vue";
export default {
  name: "App",
  components: { choosePopup, myResult },

  data() {
    return {
      gameIsOver: false,
      timeoutActive: false,
      userChoice: "",
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
          const winner =
            this.gameBoard[a] === this.computerChoice ? "Computer" : "You";
          setTimeout(this.displayWinner, 500, winner);

          return;
        }
      }
      !this.gameBoard.includes("") ? this.displayTie() : undefined;
    },
    computerPlay() {
      if (!this.gameIsOver) {
        let emptySquares = this.gameBoard
          .map((g, i) => (g === "" ? i : undefined))
          .filter((i) => i !== undefined);

        let randomIndex =
          emptySquares[Math.floor(Math.random() * emptySquares.length)];
        this.gameBoard[randomIndex] = this.computerChoice;
        this.checkforWin();
      }
    },
    displayWinner(winner) {
      this.gameIsOver = true;
      this.message = winner + ` Win${winner == "You" ? "" : "s"} the game`;
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
  computed: {
    computerChoice() {
      return this.userChoice === "X" ? "O" : "X";
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
  flex-direction: column;
  position: relative;
}
.status-container strong {
  font-size: x-large;
}
</style>
