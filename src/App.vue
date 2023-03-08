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


