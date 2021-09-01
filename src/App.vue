<template>
  <div id="app">
    <div class="wrapper clearfix">
      <players
        v-bind:scorePlayers="scorePlayers"
        v-bind:currentScore="currentScore"
        v-bind:activePlayer="activePlayer"
      />
      <controllers v-on:newGame="handleNewGame" />
      <dices />
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
      activePlayer: 1,
      scorePlayers: [14, 25],
      currentScore: 20
    };
  },
  components: {
    Players,
    Controllers,
    Dices,
    ModalRules
  },
  methods: {
    handleNewGame() {
      this.isOpenModal = true;
    },
    startNewGame() {
      this.isOpenModal = false;
      // console.log("start newgame");
      this.isPlaying = true;
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
