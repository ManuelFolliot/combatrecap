<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <PresentationCombat />

</template>





<script>
import PresentationCombat from './components/PresentationCombat.vue'


export default {
  name: 'App',
  components: {
    PresentationCombat,

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
