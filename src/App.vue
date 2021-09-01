<template>
  <div id="app">
    <div class="wrapper clearfix">
      <players
        v-bind:scorePlayers="scorePlayers"
        v-bind:currentScore="currentScore"
        v-bind:activePlayer="activePlayer"
      />
      <controllers
        v-on:newGame="handleNewGame"
        v-on:rollDice="handleRollDice"
        v-on:holdScore="handleHoldScore"
        v-bind:finalScore="finalScore"
        v-on:changeFinalScore="changeFinalScore"
        v-bind:isPlaying="isPlaying"
      />
      <dices v-bind:dices="dices" />
      <modal-rules
        v-bind:isOpenModal="isOpenModal"
        v-on:confirmRules="startNewGame"
      />
    </div>
  </div>
</template>

<script>
import Players from "./components/Players.vue";
import Controllers from "./components/Controllers.vue";
import Dices from "./components/Dices.vue";
import ModalRules from "./components/ModalRules.vue";

export default {
  name: "app",
  data() {
    return {
      isPlaying: false,
      isOpenModal: false,
      activePlayer: 0,
      scorePlayers: [14, 25],
      currentScore: 20,
      finalScore: 50,
      ////////////////////////////////
      dices: [1, 4]
    };
  },
  components: {
    Players,
    Controllers,
    Dices,
    ModalRules
  },
  methods: {
    swapPlayer() {
      this.activePlayer == 0
        ? (this.activePlayer = 1)
        : (this.activePlayer = 0);
      this.currentScore = 0;
    },
    handleNewGame() {
      this.isOpenModal = true;
    },
    startNewGame() {
      this.isOpenModal = false;
      // console.log("start newgame");
      this.isPlaying = true;
      this.dices = [6, 6];
      this.scorePlayers = [0, 0];
      this.currentScore = 0;
    },
    handleRollDice() {
      if (this.isPlaying) {
        // console.log("Roll");
        var dice1 = Math.round(Math.random() * 5 + 1);
        var dice2 = Math.round(Math.random() * 5 + 1);
        this.dices = [dice1, dice2];
        // check swap player : one of 2 == 1
        if (dice1 == 1 || dice2 == 1) {
          //swap player :
          let currentPlayer = this.activePlayer;
          setTimeout(() => {
            alert(`${currentPlayer ? "Player 2" : "Player 1"} roll in 1`);
          }, 100);

          this.swapPlayer();
        } else {
          this.currentScore += dice1 + dice2;
        }
      } else {
        alert("Click New Game !");
      }
    },
    handleHoldScore() {
      if (this.isPlaying) {
        console.log(
          "Hold",
          this.currentScore,
          this.activePlayer ? "Player 2" : "Player 1",
          this.activePlayer
        );
        let currentPlayer = this.activePlayer;
        // this.scorePlayers[currentPlayer] += this.currentScore; // khong dung dc nhu nay
        this.$set(
          this.scorePlayers,
          currentPlayer,
          this.scorePlayers[currentPlayer] + this.currentScore
        );
        //swapPlayer();
        setTimeout(() => {
          this.swapPlayer();
        }, 100);
      } else {
        alert("Click New Game !");
      }
    },
    changeFinalScore(data) {
      // console.log("changeFinalScore", data);
      if (!this.isPlaying) {
        let val = parseInt(data.value);
        this.finalScore = val;
      }
    }
  }
};
</script>

<style>
/**********************************************
*** GENERAL
**********************************************/

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("./assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
