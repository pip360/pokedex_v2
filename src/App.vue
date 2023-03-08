<template>
  <!-- home -->
  
  <div id="app">
    <pokemon-navbar/>
    <pokemon-home/>
  </div>
</template>

<script>
import PokemonHome from './components/PokemonHome.vue' 
import PokemonNavbar from './components/PokemonNavbar.vue'

export default {
  components: {
    PokemonHome,
    PokemonNavbar
  },
};
</script>

<style lang="scss">
  @import url('https://use.fontawesome.com/releases/v5.8.2/css/all.css');

  body {
    margin: 0;
    padding: 0;
  }
</style>
