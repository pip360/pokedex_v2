<template>
  <!-- modal axios -->
  <div
    class="d-flex justify-content-center align-items-start position-fixed top-0 left-0 p-9"
    style="
      background-color: rgba(25, 22, 24, 0.7);
      width: calc(100% - 20px);
      height: calc(100vh - 0px);
    "
    tabindex="-1"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <!-- modal body -->
        <div class="modal-body d-flex">
          <!-- imagen -->
          <div
          class="modal body d-flex justify-content-center align-items-center flex-column position-relative w-100 mw p-1 bg-white rounded mw-510"
          >
            <!-- modal header -->
            <div
            class="text-center mt-2 text-capitalize"
            >
            <h2 class="modal-title">Detalles de {{ pokemon_info.name }}</h2>
          </div>
          
          <img
          class="d-flex justify-content-center align-items-center bg-dark rounded-circle overflow-hidden w-150 h-150"
          
          width="100"
          height="100"
          :src="pokemon_info.urldefault.front_default"
          />
          
            <div
              class="display-flex justify-content-start align-items-center flex-column w-100 mb-40"
            >
              <!-- name -->
              <h2 class="mt-3 text-capitalize text-center">
                {{ pokemon_info.name }}
              </h2>
              <!-- XP -->
              <div class="w-90 mw-400 border-bottom-1 border-white mb-b10">
                <div class="ms-2 float-start">Experiencia</div>
                <div class="me-2 text-end">{{ pokemon_info.xp }} XP</div>
              </div>
              <!-- alura -->
              <div class="w-90 mw-400 border-bottom-1 border-white mb-b10">
                <div class="ms-2 float-start">Altura</div>
                <div class="me-2 text-end">
                  {{ pokemon_info.height / 10 }} m
                </div>
              </div>
              <!-- peso -->
              <div class="w-90 mw-400 border-bottom-1 border-white mb-b10">
                <div class="ms-2 float-start">Peso</div>
                <div class="me-2 text-end">
                  {{ pokemon_info.weight / 10 }} kg
                </div>
              </div>
              <!-- tipo -->
              <h5 class="me-2 text-center">Tipo</h5>
              <div class="types">
                <div
                  class=" rounded-pill text-white fs-6 lh-lg text-capitalize text-break p-5-10 mt-2 text-center bg-dark"
                  v-for="(pokemon, i) in pokemon_info.types"
                  :key="i"
                >
                  {{ pokemon.type.name }}
                </div>
              </div>
              <!-- abilities -->
              <h5 class="me-2 text-center mt-2">Habilidades</h5>
              <div class="d-flex justify-content-start text-wrap w-90 mw-400">
                <div
                  class="me-2 aling-items-center rounded-pill text-white fs-6 lh-lg text-capitalize text-break p-5-10 mt-2 text-center bg-dark"
                  v-for="(pokemon, i) in pokemon_info.abilities"
                  :key="i"
                >
                  {{ pokemon.ability.name }}
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


