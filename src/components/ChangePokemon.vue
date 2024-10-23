<script>
import axios from "axios";

export default {
  data() {
    return {
      apiCall: 'https://pokeapi.co/api/v2/pokemon/',
      urlPokemonImg: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
      pokemonName: '',

    }
  }, 
  props: {
    pokemonIdRandom: {
        type: Number
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

    getPokemonImg() {
        this.urlPokemonImg = this.urlPokemonImg + this.pokemonIdRandom + '.png'
        console.log(this.urlPokemonImg)
    }
  },
  created() {

  },
  mounted() {
    this.getPokemonName()
    this.getPokemonImg()
  }
}
</script>

<template>
    <div class="pokemon-to-guess mt-3">
      <div class="pokemon-image">
        <img class="pkm-img" :src="urlPokemonImg" alt="">
      </div>
      <div class="pokemon-question mt-3">
        <section>
          Which type is {{pokemonName}}?
        </section>
      </div>
    </div>
</template>

<style scoped>
</style>