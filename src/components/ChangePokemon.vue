<script>
import axios from "axios";

export default {
  data() {
    return {
      apiCall: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonName: '',
      pokemonIdRandom: 0,
      pokemonFromId: [],
    }
  }, 
  methods: {
    getPokemonName() {
        // Unisci l'api generale al numero random creato
        this.apiCall = this.apiCall + this.pokemonIdRandom;
        axios.get(this.apiCall)
            .then((response) => {
                // Assegna il nome al Pokemon
                console.log(this.apiCall)
                console.log(response.data.forms[0].name)
                this.pokemonName = response.data.forms[0].name;
        })
    },
    getRandomPokemonId() {
        this.pokemonIdRandom = Math.floor(Math.random() * 1025) + 1
    },
  },
  created() {
    this.getRandomPokemonId()
  },
  mounted() {
    this.getPokemonName()
  }
}
</script>

<template>
    <div class="pokemon-to-guess">
      <div class="pokemon-image">
        <img src="https://www.pokemon.com/static-assets/content-assets/cms2/img/pokedex/full/257.png" alt="blaziken">
      </div>
      <div class="pokemon-question">
        <section>
          Which type is {{pokemonName}}?
        </section>
      </div>
    </div>
</template>

<style scoped>
</style>