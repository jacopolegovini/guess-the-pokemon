<script>
import axios from "axios";

export default {
  data() {
    return {
      apiCall: 'https://pokeapi.co/api/v2/pokemon/torchic',
      pokemonName: '',
      pokemonIdRandom: 0,
      pokemonFromId: [],
    }
  }, 
  methods: {
    getPokemonName() {
        axios.get(this.apiCall)
            .then((response) => {
                // Individua il nome corretto per l'id random arrivato
                this.pokemonFromId = 
                console.log(this.pokemonIdRandom)
                // Assegna il nome al Pokemon
                console.log(response.data.forms[0].name)
                this.pokemonName = response.data.forms[0].name;
        })
    },
    getRandomPokemonId() {
        this.pokemonId = Math.floor(Math.random() * 1302) + 1
    },
  },
  mounted() {
    this.getPokemonName()
    this.getRandomPokemonId()
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