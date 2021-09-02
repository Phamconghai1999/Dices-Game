<template>
  <div id="app">
    <div class="wrapper clearfix">
      <players
        v-bind:scorePlayers="scorePlayers"
        v-bind:currentScore="currentScore"
        v-bind:activePlayer="activePlayer"
        v-bind:isPlaying="isPlaying"
        v-bind:checkWinner="checkWinner"
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
        v-bind:isOpenModalRules="isOpenModalRules"
        v-on:confirmRules="startNewGame"
      />
      <toast v-bind:showToast="showToast" v-bind:messageToast="messageToast" />
    </div>
  </div>
</template>

<script>
import Players from "./components/Players.vue";
import Controllers from "./components/Controllers.vue";
import Dices from "./components/Dices.vue";
import ModalRules from "./components/ModalRules.vue";
import Toast from "./components/Toast.vue";

export default {
  name: "app",
  data() {
    return {
      isPlaying: false,
      isOpenModalRules: false,
      activePlayer: 0,
      scorePlayers: [2, 8],
      currentScore: 20,
      finalScore: 30,
      ////////////////////////////////
      dices: [1, 4],
      //== Show notification
      showToast: false,
      messageToast: ""
    };
  },
  components: {
    Players,
    Controllers,
    Dices,
    ModalRules,
    Toast
  },
  computed: {
    checkWinner: function() {
      let { scorePlayers, finalScore } = this;
      if (scorePlayers[0] >= finalScore || scorePlayers[1] >= finalScore) {
        this.isPlaying = false;
        // console.log("Winner: Player", this.activePlayer);
        let Winner = this.activePlayer;
        return { isWinner: true, Winner };
      }
      return { isWinner: false, Winner: null };
    }
  },
  methods: {
    swapPlayer() {
      this.activePlayer == 0
        ? (this.activePlayer = 1)
        : (this.activePlayer = 0);
      this.currentScore = 0;
    },
    notification(message) {
      this.showToast = true;
      this.messageToast = message;
      setTimeout(() => {
        this.showToast = false;
      }, 3000);
    },
    handleNewGame() {
      this.isOpenModalRules = true;
    },
    startNewGame() {
      this.isOpenModalRules = false;
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
            this.notification(
              `${currentPlayer ? "Player 2" : "Player 1"} roll in 1`
            );
          }, 100);

          this.swapPlayer();
        } else {
          this.currentScore += dice1 + dice2;
        }
      } else {
        this.notification("Click New Game First !!!");
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
        //check winner
        if (this.checkWinner.isWinner == false) {
          this.swapPlayer();
        }
      } else {
        this.notification("Click New Game First !!!");
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
