<template>
  <div id="app">
    <mainmenu msg="Contact information system"/>
  </div>
</template>

<script>
import mainmenu from './components/mainmenu.vue'

export default {
  name: 'app',
  components: {
    mainmenu
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
