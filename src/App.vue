<template>
  <div id="app">
    <ColorSetting />
  </div>
</template>

<script>
import ColorSetting from './components/colorSetting/index.vue'

export default {
  name: 'App',
  components: {
    ColorSetting
  }
}
</script>

<style>
html {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #f2f2f2;
}
</style>
