<template>
  <!-- modal axios -->
  <div class="modal" tabindex="-1">
    <div class="modal-dialog">
      <div class="modal-content">
        <!-- modal header -->
        <div class="modal-header">
          <h2 class="modal-title">Detalles de {{ pokemon_info.name }}</h2>

          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
            @click="$emit('close')"
          ></button>
        </div>
        <!-- modal body -->
        <div class="modal-body">
          <!-- imagen -->
          <div class="modal-view">
            <img class="image"
            width="100"
            height="100"
            :src="pokemon_info.urldefault.front_default" />
            <div class="data">
              <!-- name -->
              <h2 class="mt-3">{{ pokemon_info.name }}</h2>
              <!-- XP -->
              <div class="property">
                <div class="left">Experiencia</div>
                <div class="right">{{ pokemon_info.xp }} XP</div>
              </div>
              <!-- alura -->
              <div class="property">
                <div class="left">Altura</div>
                <div class="right">{{ pokemon_info.height / 10 }} m</div>
              </div>
              <!-- peso -->
              <div class="property">
                <div class="left">Peso</div>
                <div class="right">{{ pokemon_info.weight / 10 }} kg</div>
              </div>
              <!-- tipo -->
              <h3>Tipo</h3>
              <div class="types">
                <div
                  class="type"
                  v-for="(pokemon, i) in pokemon_info.types"
                  :key="i"
                >
                  {{ pokemon.type.name }}
                </div>
              </div>
              <!-- abilities -->
              <h3>Habilidades</h3>
              <div class="abilities">
                <div
                  class="ability"
                  v-for="(pokemon, i) in pokemon_info.abilities"
                  :key="i"
                >
                  {{ pokemon.ability.name }}
                </div>
              </div>
            </div>

          </div>
        </div>
        <!-- modal footer -->
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-dark"
            data-bs-dismiss="modal"
            @click="$emit('close')"
          >
            Cerrar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* axios */
export default {
  props: {
    pokemon_info: [],
  },
  data() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.modal-header h2:first-letter {
  text-transform: uppercase;
}

.modal-header h2 {
  text-transform: lowercase;
}
.modal {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: fixed;
  top: 0;
  left: 0;
  padding: 90px 10px 10px;
  width: calc(100% - 20px);
  height: calc(100vh - 20px);
  background: rgba($color: #000000, $alpha: 0.7);

  .modal-view {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    position: relative;
    width: 100%;
    max-width: 510px;
    padding: 1px;
    background-color: #fff;
    border-radius: 5px;

    .image {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 150px;
      height: 150px;
      background-color: #333333e8;
      border-radius: 50%;
      overflow: hidden;
      
    }

    h2 {
      text-transform: capitalize;
    }

    .data {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      flex-direction: column;
      width: 100%;
      margin-bottom: 40px;

      .property {
        width: 90%;
        max-width: 400px;
        border-bottom: 1px solid #ccc;
        margin-bottom: 10px;

        .left {
          float: left;
        }
        .right {
          float: right;
        }
      }

      h3 {
        width: 90%;
        max-width: 400px;
        border-bottom: 1px solid #ccc;
      }

      .types,
      .abilities {
        display: flex;
        justify-content: flex-start;
        flex-wrap: wrap;
        width: 90%;
        max-width: 400px;

        .ability {
          margin: 0 10px 10px 0;
          padding: 5px 10px;
          border-radius: 20px;
          color: #fff;
          font-size: 1rem;
          letter-spacing: 2px;
          text-transform: capitalize;
          word-wrap: none;
          word-break: keep-all;
        }

        .type {
          background-color: #dbdfe3;
          margin: 0 10px 10px 0;
          padding: 5px 10px;
          border-radius: 20px;
          color: #ffffff;
          font-size: 1rem;
          letter-spacing: 2px;
          text-transform: capitalize;
          word-wrap: none;
          word-break: keep-all;
        }
        .ability {
          background-color: #a1a1a1;
        }
      }
    }

    .close {
      outline: none;
      border: none;
      border-radius: 5px;
      background-color: #333;
      color: #efefef;
      padding: 10px 20px;
      margin-bottom: 20px;
      font-size: 1.2rem;
      cursor: pointer;
    }
  }

  i {
    font-size: 2rem;
    color: #efefef;
  }
}
</style>
