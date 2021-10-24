<template>
  <div class="popup">
    <div class="modal-background" @click="hide">
    </div>
    <div class="modal-popup">
      <iframe :src="popupSrc"/>
      <a href="javascript: void(0);" class="modal-close" @click="hide">x</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    visible: Boolean,
    popupSrc: String,
  },
  methods: {
    hide() {
      this.$emit('onHide');
    },
  },
}
</script>

<style scoped lang="scss">
@media only screen and (min-width: 768px) {
  .popup {
    .modal-popup {
      width: 1024px;
      height: 786px;

      iframe {
        width: 1024px;
        height: 786px;
      }
    }
  }
}
@media only screen and (max-width: 768px) {
  .popup {
    .modal-popup {
      width: 320px;
      height: 240px;
      iframe {
        width: 320px;
        height: 240px;
      }
    }
  }
}
.popup {
  position: fixed;
  top: 0px;
  left: 0px;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  .modal-background {
    opacity: 0.5;
    position: fixed;
    top: 0px;
    left: 0px;
    height: 100vh;
    width: 100vw;
    background-color: black;
  }
  .modal-popup {
    position: fixed;
    background-color: white;
    opacity: 1;
    iframe {
      border: 0px solid white;
    }
    .modal-close {
      position: absolute;
      top: 10px;
      right: 10px;
      display: block;
      width: 36px;
      height: 36px;
      text-align: center;
      line-height: 36px;
      text-decoration: none;
      color: white;
      background-color: black;
      opacity: 0.5;
      font-size: 22px;
    }
  }
}
</style>
