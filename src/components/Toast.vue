<template lang="">
  <div class="toast" v-bind:class="showToastComputed">
    <div class="toast-header">
      <img
        src="https://www.logolynx.com/images/logolynx/1a/1aaf01cfac3a67d919cac9d091c7da72.png"
        class="rounded mr-2 logo"
        alt="logo toast"
      />
      <strong class="mr-auto">-!!!-</strong>
    </div>
    <div class="toast-body">
      {{ messageToast }}
    </div>
  </div>
</template>
<script>
export default {
  name: "toast",
  data() {
    return {};
  },
  props: {
    showToast: {
      Type: Boolean,
      default: false
    },
    messageToast: {
      Type: String,
      default: ""
    }
  },
  computed: {
    showToastComputed: function() {
      return { show: this.showToast };
    }
  }
};
</script>
<style lang="">
.toast {
  position: absolute;
  top: 5px;
  right: 5px;
  margin: 1em;
  padding: 5px;
  background: rgba(45, 253, 97, 0.14);
  font: 18px sans-serif;
  z-index: 99;
  border: 1px solid black;
  border-radius: 5px;
  transition: all 0.3s ease;
  opacity: 0;
  visibility: hidden;
}

.toast.show {
  opacity: 1;
  visibility: visible;
}

.toast .logo {
  height: 2em;
}
</style>
