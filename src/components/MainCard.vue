<script>
import ChangePokemon from './ChangePokemon.vue';
import axios from 'axios';

export default {
  data() {
    return {
      apiCall: 'https://pokeapi.co/api/v2/pokemon/blaziken',
      pokemonName: '',
    }
  },
  methods: {
    getApi() {
        axios.get(this.apiCall)
            .then((response) => {
                console.log(response.data.forms[0].name)
                this.pokemonName = response.data.forms[0].name;
                this.pokemonName = this.pokemonName;
        })
    },
  },
  mounted() {
    this.getApi()
  },
  components: {
    ChangePokemon
  }
}
</script>

<template>
  <!-- Components -->
  <ChangePokemon />

  <!-- Headers -->
  <header>
    <div class="title">
      <h1>Guess The Pokemon</h1>
    </div>
  </header>

  <!-- Main -->
  <main>
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
    <div class="answer">
      <form action="">
        <select name="pokemon-type" id="pokemon-type">
          <option value="fire">Fire</option>
          <option value="fighting">Fighting</option>
        </select>
        <button>I'm sure!</button>
      </form>
    </div>
  </main>
</template>

<style scoped>
</style>