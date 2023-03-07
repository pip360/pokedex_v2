<template>
  <!-- anterior -->
  <div class="list">
    <!-- <div 
      class="card"
      v-for="(pokemon, index) in pokemons"
      :key="'poke' + index"
    >
      <img
        :src="imageUrl + pokemon.id + '.png'"
        width="96"
        height="96"
        alt=""
      />
      <div class="card-body">
        <h3 class="card-title">{{ pokemon.name }}</h3>
        <a class="btn btn-dark" @click="setPokemonUrl(pokemon.url)">
          Detalles
        </a>
      </div>
    </div>
    <div id="scroll-trigger" ref="infinitescrolltrigger">
      <i class="fas fa-spinner fa-spin"></i>
    </div> -->
  </div>
  <!-- axios -->
  <div class="list">
    <div class="card" v-for="(data, index) in pokemons" :key="index">
      <img :src="data.url.front_default" @click="send_info(data)"/>
      <div class="card-body">
        <h3 class="card-title">{{ data.name }}</h3>
        <a class="btn btn-dark" @click="showPokedetails(data)">
          Detalles
        </a>
      </div>
    </div>
    <!-- mostrar modal -->
    <modal :pokemon_info="selected_pokemon" v-if="showModal" @close="showModal = false"/>
  </div>
</template>

<script>
import axios from "axios";
import Modal from './PokemonModal.vue';
/* import { response } from 'express'; */
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
            name: response.data.name,
          };
          instance.pokemons.push(pokemon);
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
/* anterior */
/* export default {
  props: ["imageUrl", "apiUrl"],
  data: () => {
    return {
      pokemons: [],
      nextUrl: "",
      currentUrl: "",
    };
  },
  methods: {
    fetchData() {
      let req = new Request(this.currentUrl);
      fetch(req)
        .then((resp) => {
          if (resp.status === 200) return resp.json();
        })
        .then((data) => {
          this.nextUrl = data.next;
          data.results.forEach((pokemon) => {
            pokemon.id = pokemon.url
              .split("/")
              .filter(function (part) {
                return !!part;
              })
              .pop();
            this.pokemons.push(pokemon);
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
    
    scrollTrigger() {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.intersectionRatio > 0 && this.nextUrl) {
            this.next();
          }
        });
      });

      observer.observe(this.$refs.infinitescrolltrigger);
    },
    next() {
      this.currentUrl = this.nextUrl;
      this.fetchData();
    },
    setPokemonUrl(url) {
      this.$emit("setPokemonUrl", url);
    },
  },
  created() {
    this.currentUrl = this.apiUrl;
    this.fetchData();
  },
  mounted() {
    this.scrollTrigger();
  },
}; */
</script>

<style lang="scss" scoped>
.card-body h3:first-letter {
  text-transform: uppercase;
}

.card-body h3 {
  text-transform: lowercase;
}
.card {
  transition: transform 0.5s;
}

.card:hover {
  transform: scale(1.07);
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

#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}
</style>

