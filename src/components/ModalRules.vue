<template lang="">
  <div class="wrapper-rules" v-bind:class="isOpenModalComputed">
    <div class="rules">
      <h3>Rule:</h3>
      <p>
        Lorem ipsum dolor sit amet, consectet dolore eu fugiat nulla pariatur et
      </p>
      <button class="btn btn-success" v-on:click="confirmRules">
        Okey !
      </button>
    </div>
  </div>
</template>
<script>
export default {
  name: "modal-rule",
  props: {
    isOpenModal: {
      Type: Boolean,
      default: false
    }
  },
  computed: {
    isOpenModalComputed: function() {
      return {
        "open-modal": this.isOpenModal
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
  text-align: center;
  margin: 10px 10px;
  padding: 10px 10px;
  border: 1px solid rgb(116, 255, 111);
  border-radius: 13px;
  font: 25px sans-serif;
  transition: all 0.3s ease;
}
</style>
