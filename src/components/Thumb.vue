<template>
  <div>
    <div class="thumb-container" @click="openPreivewPopup">
      <img :src="responsiveUrl" class="thumb"/>
    </div>
    <div class="thumb-info">
      <span class="thumb-author" :title="author">{{ author }}</span>
      <div class="thumb-id">#{{ id }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Thumb",
  props: {
    author: String,
    responsiveUrl: String,
    srcUrl: String,
    id: String,
  },
  methods: {
    openPreivewPopup: function() {
      this.$emit('onClick', {srcUrl: this.srcUrl});
    },
  },
};
</script>

<style scoped lang="scss">
  div {
    -webkit-box-shadow: 10px 10px 11px -7px rgba(36, 36, 36, 0.25);
    -moz-box-shadow: 10px 10px 11px -7px rgba(36, 36, 36, 0.25);
    box-shadow: 10px 10px 11px -7px rgba(36, 36, 36, 0.25);
    margin: 10px;
    border: 1px solid #eee;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    .thumb-container {
      width: 320px;
      height: auto;
      padding: 0px;
      margin: 0px;
      box-sizing: border-box;
      .thumb {
        width: auto;
        height: auto;
        max-width: 100%;
        max-height: 100%;
      }
    }
    .thumb-info {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      padding: 15px;
      box-sizing: border-box;
      box-shadow: none;
      border: none;
      .thumb-id, .thumb-author {
        margin: 0px;
        padding: 5px;
        box-sizing: border-box;
        box-shadow: none;
        border: none;
      }
      .thumb-id {
        border-radius: 16px;
        background-color: #f1f5f8;
        padding-left: 10px;
        padding-right: 10px;
        font-family: 'Open Sans', sans-serif;
        font-weight: normal;
      }
      .thumb-author {
        align-items: flex-start;
        max-width: 205px;
        width: 205px;
        text-align: left;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }
    }
  }
</style>
