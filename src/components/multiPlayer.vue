<template>
  <section class="container">
    <div class="top-container">
      <div class="score-board">
        <div :class="{ activeUser: activeUser == 'X' }" class="player-stats">
          <strong>{{ playerXScore }}</strong>
          Player X
          <div v-if="activeUser == 'X'" class="X player-bar"></div>
        </div>
        <hr />
        <div :class="{ activeUser: activeUser == 'O' }" class="player-stats">
          <strong>{{ playerOScore }}</strong>
          Player O
          <div v-if="activeUser == 'O'" class="O player-bar"></div>
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
    <button class="return" @click="$emit('refresh')">Return to menu</button>
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
      const ls = this;
      this.winningCombinations.map((combination) => test(combination));
      function test(combination) {
        const [a, b, c] = combination;
        console.log(a, b, c);
        if (
          ls.gameBoard[a] &&
          ls.gameBoard[a] === ls.gameBoard[b] &&
          ls.gameBoard[b] === ls.gameBoard[c]
        ) {
          ls.displayWinner();
          ls.changeUser();

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
<style>
.X {
  right: 0;
  position: absolute;
}
.O {
  left: 0;
  position: absolute;
}
</style>
