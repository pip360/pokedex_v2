<template>
  <div>
    <pokemon-banner />

    
    <div
      class="container d-flex justify-content-center align-items-center flex-column p-10"
    >
      <pokemon-list />
      <pokemon-modal v-if="showDetail" />
    </div>
    <poke-footer />
  </div>
</template>

<script>
import PokemonList from "./PokemonList.vue";
import PokemonModal from "./PokemonModal.vue";
import PokemonBanner from "./PokemonBanner.vue";
import PokeFooter from "./PokeFooter.vue";

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
    PokeFooter,
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

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Fresca&display=swap");
.container {
  font-family: "Fresca", sans-serif;
  font-size: 1rem;
  font-weight: normal;
}
</style>
