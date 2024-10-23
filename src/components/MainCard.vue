<script>
import ChangePokemon from './ChangePokemon.vue';
import axios from 'axios';

export default {
  data() {
    return {
      apiCall: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonTypes: [],
      typeChosen: '',
      secondTypeChosen: '',
      typeChosenIsCorrect: false,
      answerDone: false,
      pokemonIdRandom: 0,
    }
  },
  methods: {
    getApi() {
      this.apiCall = this.apiCall + this.pokemonIdRandom;
        axios.get(this.apiCall)
            .then((response) => {
                // Estra il tipo del pokemon e lo assegna alla variabile
                console.log(response.data.types)
                this.pokemonTypes = response.data.types;
                console.log(this.apiCall)
        })
    },
    isAnswerRight(answer, secondAnswer = null) {
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
        // Se il pokemon ha due tipi
        if ((answer === this.pokemonTypes[0].type.name && secondAnswer === this.pokemonTypes[1].type.name) || (answer === this.pokemonTypes[1].type.name && secondAnswer === this.pokemonTypes[0].type.name)) {
          console.log('Il tipo è giusto')
          this.typeChosenIsCorrect = true;
          console.log(this.typeChosenIsCorrect)
        } else {
          console.log('Il tipo è sbagliato')
          this.typeChosenIsCorrect = false;
          console.log(this.typeChosenIsCorrect)
        }
      }
      this.answerDone = true;
    },
    getRandomPokemonId() {
        this.pokemonIdRandom = Math.floor(Math.random() * 1025) + 1
    },
    getAgainRandomPokemonId() {
        return Math.floor(Math.random() * 1025) + 1
    },
  },
  beforeMount() {
    this.getRandomPokemonId()
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
  <!-- Headers -->
  <header>
    <div class="title">
      <h1>Guess The Pokemon</h1>
    </div>
  </header>

  <!-- Main -->
  <main>

    <div class="d-flex justify-content-center flex-column align-center">
      <!-- Question -->
      <ChangePokemon 
        :pokemonIdRandom="pokemonIdRandom"/>
  
      <!-- Answer -->
      <div class="answer my-2 d-flex flex-column">
        <form action="" class="d-flex gap-2">
          <select class="select-style form-select" name="pokemon-type" id="pokemon-type" v-model="typeChosen">
            <option value="normal">Normal</option>
            <option value="fire">Fire</option>
            <option value="water">Water</option>
            <option value="electric">Electric</option>
            <option value="grass">Grass</option>
            <option value="ice">Ice</option>
            <option value="fighting">Fighting</option>
            <option value="poison">Poison</option>
            <option value="ground">Ground</option>
            <option value="flying">Flying</option>
            <option value="psychic">Psychic</option>
            <option value="bug">Bug</option>
            <option value="rock">Rock</option>
            <option value="ghost">Ghost</option>
            <option value="dragon">Dragon</option>
            <option value="dark">Dark</option>
            <option value="steel">Steel</option>
            <option value="fairy">Fairy</option>
          </select>
          <select class="select-style form-select" name="pokemon-type" id="pokemon-type" v-model="secondTypeChosen" v-if="pokemonTypes.length === 2">
            <option value="normal">Normal</option>
            <option value="fire">Fire</option>
            <option value="water">Water</option>
            <option value="electric">Electric</option>
            <option value="grass">Grass</option>
            <option value="ice">Ice</option>
            <option value="fighting">Fighting</option>
            <option value="poison">Poison</option>
            <option value="ground">Ground</option>
            <option value="flying">Flying</option>
            <option value="psychic">Psychic</option>
            <option value="bug">Bug</option>
            <option value="rock">Rock</option>
            <option value="ghost">Ghost</option>
            <option value="dragon">Dragon</option>
            <option value="dark">Dark</option>
            <option value="steel">Steel</option>
            <option value="fairy">Fairy</option>
          </select>
        </form>
        <button class="btn btn-primary my-2" @click="isAnswerRight(typeChosen, secondTypeChosen)">I'm sure!</button>
      </div>
  
      <!-- Result -->
      <div class="result" v-if="answerDone">
        <div class="right-answer text-primary" v-if="typeChosenIsCorrect">
          <p>Right answer!</p>
        </div>
        <div class="wrong-answer text-danger" v-else>
          <p>Wrong answer!</p>
        </div>
      </div>
  
      <!-- Play again -->
      <div class="play-again" v-if="answerDone">
        <button class="btn btn-secondary" @click="pokemonIdRandom = getAgainRandomPokemonId(), console.log(pokemonIdRandom), getApi()">Play Again</button>
      </div>
    </div>
</main>
</template>

<style scoped>
</style>