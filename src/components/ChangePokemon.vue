<script>
import axios from "axios";

export default {
  data() {
    return {
      apiCall: 'https://pokeapi.co/api/v2/pokemon/',
      urlPokemonImg: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
      pokemonName: '',
      pokemonIdRandom: 0,
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
    getPokemonImg() {
        this.urlPokemonImg = this.urlPokemonImg + this.pokemonIdRandom + '.png'
        console.log(this.urlPokemonImg)
    }
  },
  created() {
    this.getRandomPokemonId()
  },
  mounted() {
    this.getPokemonName()
    this.getPokemonImg()
  }
}
</script>

<template>
    <div class="pokemon-to-guess">
      <div class="pokemon-image">
        <img :src="urlPokemonImg" alt="blaziken">
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