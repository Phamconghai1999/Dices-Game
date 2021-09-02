<template lang="">
  <div class="wrapper-rules" v-bind:class="isOpenModalRulesComputed">
    <div class="rules">
      <h4>Luật chơi:</h4>
      <p>1. Bấm RollDice để lắc xúc xắc</p>
      <p>2. Nếu xúc xắc trúng ô điểm 1, bạn sẽ bị mất lượt</p>
      <p>3. Bấm HOLD để giữ lại điểm và chuyển lượt chơi</p>
      <button class="btn btn-primary" v-on:click="confirmRules">
        Okey, Let's go !!
      </button>
    </div>
  </div>
</template>
<script>
export default {
  name: "modal-rule",
  props: {
    isOpenModalRules: {
      Type: Boolean,
      default: false
    }
  },
  computed: {
    isOpenModalRulesComputed: function() {
      return {
        "open-modal": this.isOpenModalRules
      };
    }
  },
  methods: {
    confirmRules: function() {
      this.$emit("confirmRules");
    }
  },
  data() {
    return {};
  }
};
</script>
<style lang="">
.wrapper-rules {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6);
  opacity: 0;
  transition: all 0.3s ease;
  visibility: hidden;
}
.wrapper-rules.open-modal {
  opacity: 1;
  visibility: visible;
}
.open-modal .rules {
  transform: translate(-50%, -50%) scale(1);
}
.rules {
  position: absolute;
  width: 300px;
  height: 200px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(1.2);
  background: rgb(255, 227, 227);
  text-align: left;
  margin: 10px 10px;
  padding: 10px 10px;
  border: 1px solid rgb(116, 255, 111);
  border-radius: 13px;
  font: 15px sans-serif;
  transition: all 0.3s ease;
}
.rules p {
  padding: 1px 1px;
  margin: 2px 2px;
}
.rules button {
  position: relative;
  margin: auto 50%;
}
</style>
