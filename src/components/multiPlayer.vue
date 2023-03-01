<template>
  <section class="container">
    <div class="top-container">
      <div class="score-board">
        <div :class="{ activeUser: activeUser == 'X' }" class="">
          <strong>{{ playerXScore }}</strong>
          Player X
        </div>
        <hr />
        <div :class="{ activeUser: activeUser == 'O' }" class="">
          <strong>{{ playerOScore }}</strong>
          Player O
        </div>
      </div>
    </div>

    <div class="game">
      <my-result
        @refresh="refresh"
        v-if="gameIsOver"
        :message="message"
      ></my-result>
      <div
        :class="{ gameOver: gameIsOver }"
        :key="i"
        v-for="(area, i) in gameBoard"
        @click="handlePlay(i)"
        class="board-cell"
      >
        {{ area }}
      </div>
    </div>
  </section>
</template>

<script>
import myResult from "./myResult.vue";
export default {
  name: "App",
  components: { myResult },
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
