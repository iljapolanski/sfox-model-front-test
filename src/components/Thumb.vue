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
@media only screen and (max-width: 767px) {
  div {
    margin: 3px;
    width: 98px;
    max-width: 98px;

    .thumb-info {
      flex-direction: column-reverse;
    }

    .thumb-container {
      width: 98px;
      margin: 0px;
      padding: 0px;
    }

    .thumb-author {
      max-width: 88px;
      width: 88px;
      font-size: 10px;
    }

    .thumb-id {
      font-size: 10px;
    }
  }
}
@media only screen and (min-width: 768px) {
  div {
    margin: 10px;
    .thumb-container {
      width: 227px;
      max-width: 227px;
    }
    .thumb-info {
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
    }
    .thumb-author {
      max-width: 120px;
      width: 120px;
      font-size: 14px;
    }
    .thumb-id {
      font-size: 14px;
    }
  }
}
  div {
    -webkit-box-shadow: 10px 10px 11px -7px rgba(36, 36, 36, 0.25);
    -moz-box-shadow: 10px 10px 11px -7px rgba(36, 36, 36, 0.25);
    box-shadow: 10px 10px 11px -7px rgba(36, 36, 36, 0.25);
    border: 1px solid #eee;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    .thumb-container {
      height: auto;
      padding: 0px;
      margin: 0px;
      box-sizing: border-box;
      box-shadow: none;
      .thumb {
        width: auto;
        height: auto;
        max-width: 100%;
        max-height: 100%;
      }
    }
    .thumb-info {
      display: flex;
      align-items: center;
      width: 100%;
      padding: 15px;
      box-sizing: border-box;
      box-shadow: none;
      border: none;
      margin: 0px;
      .thumb-id, .thumb-author {
        margin: 0px;
        padding: 5px;
        box-sizing: border-box;
        box-shadow: none;
        border: none;
        width: auto;
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
        text-align: left;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }
    }
  }
</style>
