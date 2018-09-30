<template>
  <div id="app">
    <forca />
  </div>
</template>

<script>
import Forca from '@/template/Forca'

export default {
  name: 'app',
  components: {
    Forca
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
