<template>
  <images-list-main/>
</template>

<script>
import ImagesListMain from './components/ImagesListMain.vue'

export default {
  name: 'App',
  components: {
    ImagesListMain
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
