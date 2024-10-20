<script>
import ChangePokemon from './ChangePokemon.vue';
import axios from 'axios';

export default {
  data() {
    return {
      apiCall: 'https://pokeapi.co/api/v2/pokemon/torchic',
      pokemonTypes: [],
      typeChosen: '',
      typeChosenIsCorrect: false,
      answerDone: false,
    }
  },
  methods: {
    getApi() {
        axios.get(this.apiCall)
            .then((response) => {
                // Estra il tipo del pokemon e lo assegna alla variabile
                console.log(response.data.types)
                this.pokemonTypes = response.data.types;
                console.log(this.pokemonTypes[0].type.name)
        })
    },
    isAnswerRight(answer) {
      if (this.pokemonTypes.length === 1) {
        if (answer === this.pokemonTypes[0].type.name) {
          console.log('Il tipo è giusto')
          this.typeChosenIsCorrect = true;
          console.log(this.typeChosenIsCorrect)
        } else {
          console.log('Il tipo è sbagliato')
          this.typeChosenIsCorrect = false;
          console.log(this.typeChosenIsCorrect)
        }
      } else {
        console.log('Ha due tipi')
      }
      this.answerDone = true;
    },
  },
  mounted() {
  },
  components: {
    ChangePokemon
  }
}
</script>

<template>
  <!-- Headers -->
  <header>
    <div class="title">
      <h1>Guess The Pokemon</h1>
    </div>
  </header>

  <!-- Main -->
  <main>

    <!-- Question -->
    <ChangePokemon />

    <!-- Answer -->
    <div class="answer">
      <form action="">
        <select name="pokemon-type" id="pokemon-type" v-model="typeChosen">
          <option value="fire">Fire</option>
          <option value="fighting">Fighting</option>
          <option value="rock">Rock</option>
          <option value="water">Water</option>
        </select>
      </form>
      <button @click="isAnswerRight(typeChosen)">I'm sure!</button>
    </div>

    <!-- Result -->
    <div class="result" v-if="answerDone">
      <div class="right-answer" v-if="typeChosenIsCorrect">
        <p>Right answer!</p>
      </div>
      <div class="wrong-answer" v-else>
        <p>Wrong answer!</p>
      </div>
    </div>
  </main>
</template>

<style scoped>
</style>