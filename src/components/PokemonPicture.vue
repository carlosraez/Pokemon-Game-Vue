<template>
  <div class="pokemon-container">
    <img :src="imgUrl" alt="Pokemon" class="hidden-pokemon" />
    <img v-if="showPokemon" :src="imgUrl" alt="Pokemon" class="fade-in" />
  </div>
</template>

<script>
export default {
  props: {
    pokemonID: {
      type: Number,
      required: true,
      default: 1,
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  computed: {
    imgUrl() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonID}.svg`;
    },
  },
};
</script>

<style scoped>
.pokemon-container {
  height: 200px;
}
img {
  height: 200px;
  position: absolute;
  right: 32%;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
}
.hidden-pokemon {
  filter: brightness(0);
}
</style>