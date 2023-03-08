<template>
  <!-- axios -->
  <h2>¡Explora los Pokemon!</h2><br/>
  <div class="list mt-2">
    <div class="card" v-for="(data, index) in pokemons" :key="index" @click="send_info(data), showPokedetails(data)">
      <div class="imagen">

        <img height="150" width="150" :src="data.url.front_default" />
      </div>

      <div class="card-body">
        <h6 class="card-title">{{ data.name }}</h6>
      </div>
    </div>
    <!-- mostrar modal -->
    <modal :pokemon_info="selected_pokemon" v-if="showModal" @close="showModal = false"/>
  </div>
</template>

<script>
import axios from "axios";
import Modal from './PokemonModal.vue';
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
    Modal
  },
  created() {
    let instance = this;

    for (let i = 0; i <= 5; i++) {
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
    console.log(this.pokemons)
  },
  methods: {
    showPokedetails(){
      this.showModal= true;
    }, 
    send_info(pokemon_info){
      this.selected_pokemon = pokemon_info
    }
  },
};
  
</script>

<style lang="scss" scoped>
.card-body h6:first-letter {
  text-transform: uppercase;
}

.card-body h6 {
  text-transform: lowercase;
}
.card {
  transition: transform 0.3s;
  padding: 15px;
  position: relative;
  border-radius: 20px;
  height: 210px;
  width: 160px;
  color: rgba(255, 255, 255, 0.363)000;
}

.card:hover {
  transform: scale(1.03);
}
.imagen{
  position: relative;
  right: -4px;
  border-bottom-width: 0;
  bottom: 0;
} 

.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;

  article {
    height: 150px;
    background-color: #efefef;
    text-align: center;
    text-transform: capitalize;
    border-radius: 5px;
    cursor: pointer;

    h3 {
      margin: 0;
    }
  }
}


</style>

