<template>
  <!-- axios -->
  <div
    class="list d-grid mw-510 w-100 mt-4"
    style="
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      grid-gap: 15px;
    "
  >
    <div
      class="card pe-auto p-15 position-relative rounded-3 h-210 w-160"
      style="transition: transform 0.2s"
      v-for="(data, index) in pokemons"
      :key="index"
      @click="send_info(data), showPokedetails(data)"
    >
      <div class="imagen position-relative float-start me-2 mt-1">
        <img height="150" width="150" :src="data.url.front_default" />
      </div>

      <div class="card-body text-capitalize">
        <h6 class="card-title">{{ data.name }}</h6>
      </div>
    </div>
    <!-- mostrar modal -->
    <modal
      :pokemon_info="selected_pokemon"
      v-if="showModal"
      @close="showModal = false"
    />
  </div>
</template>

<script>
import axios from "axios";
import Modal from "./PokemonModal.vue";
/* axios */
export default {
  data() {
    return {
      pokemons: [],
      showModal: false,
      selected_pokemon: [],
    };
  },
  components: {
    Modal,
  },
  created() {
    let instance = this;

    for (let i = 0; i <= 101; i++) {
      axios
        .get(`https://pokeapi.co/api/v2/pokemon/${i + 1}`)
        .then((response) => {
          let pokemon = {
            abilities: response.data.abilities,
            url: response.data.sprites.other.dream_world,
            urldefault: response.data.sprites,
            name: response.data.name,
            xp: response.data.base_experience,
            height: response.data.height,
            weight: response.data.weight,
            types: response.data.types,
          };
          instance.pokemons.push(pokemon);
          /* console.log(response.data.base_experience); */
        })
        .catch((err) => {
          console.log(err);
        });
    }
    console.log(this.pokemons);
  },
  methods: {
    showPokedetails() {
      this.showModal = true;
    },
    send_info(pokemon_info) {
      this.selected_pokemon = pokemon_info;
    },
  },
};
</script>

<style>
.card:hover {
  transform: scale(1.06);
}
</style>

