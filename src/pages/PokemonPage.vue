<template>
  <h1 v-if="!pokemon">Espere...</h1>
  <div v-else>
    <h1>¿Quien es este pokemon?</h1>
    <PokemonPicture :pokemonID="pokemon.id" :showPokemon="showPokemon" />
    <PokemonOptions @selection="checkAnswer" :pokemons="pokemonArr" />
    <template v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button @click="newGame">Nuevo Juego</button>
    </template>
  </div>
</template>

<script>
import PokemonOptions from "@/components/PokemonOptions.vue";
import PokemonPicture from "@/components/PokemonPicture.vue";
import getPokemonOptions from "@/helpers/getPokemonOptions";

export default {
  components: {
    PokemonOptions,
    PokemonPicture,
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonArry() {
      this.pokemonArr = await getPokemonOptions();
      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArr[rndInt];
    },
    checkAnswer(pokemonId) {
      this.showAnswer = true;
      if (this.pokemon.id === pokemonId) {
        this.showPokemon = true;
        this.message = `Correcto es ${this.pokemon.name}`;
      } else {
        this.message = `Es incorrecto,El pokemon era ${this.pokemon.name}`;
      }
    },
    newGame() {
      (this.pokemonArrv = []),
        (this.pokemon = null),
        (this.showPokemon = false),
        (this.showAnswer = false),
        (this.message = ""),
        this.mixPokemonArry();
    },
  },
  mounted() {
    this.mixPokemonArry();
  },
};
</script>

<style>
</style>