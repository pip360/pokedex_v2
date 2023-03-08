<template>
  <div>
    <pokemon-banner />

    <div class="container">
      
      <pokemon-list
      />
      <pokemon-modal
        v-if="showDetail"
      />
    </div>
  </div>
</template>

<script>
import PokemonList from "./PokemonList.vue";
import PokemonModal from "./PokemonModal.vue";
import PokemonBanner from "./PokemonBanner.vue";


export default {
  data: () => {
    return {
      imageUrl:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
      apiUrl: "https://pokeapi.co/api/v2/pokemon/",
      pokemonUrl: "",
      showDetail: false,
    };
  },
  components: {
    PokemonList,
    PokemonModal,
    PokemonBanner,
    
  },
  methods: {
    setPokemonUrl(url) {
      this.pokemonUrl = url;

      this.showDetail = true;
    },
    closeModal() {
      this.pokemonUrl = "";
      this.showDetail = false;
    },
  },
};
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Fresca&display=swap");

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  
  font-family: "Fresca", sans-serif;

  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #191919;
}

</style>
