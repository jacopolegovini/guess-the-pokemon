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
    pageReload() {
      location.reload();
    },
    getRandomPokemonId() {
      this.pokemonIdRandom = Math.floor(Math.random() * 1025) + 1
    },
    // TODO Trovare un modo per togliere il reload
    // getAgainRandomPokemonId() {
    //   return Math.floor(Math.random() * 1025) + 1
    // },
  },
  created() {
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
  <!-- Main -->
  <main>

    <div class="d-flex justify-content-center flex-column align-center">
      <!-- Question -->
      <ChangePokemon :pokemonIdRandom="pokemonIdRandom" />

      <!-- Answer -->
      <div class="answer my-2 d-flex flex-column">
        <form action="" class="d-flex gap-2">
          <select class="select-style form-select" name="pokemon-type" id="pokemon-type" v-model="typeChosen">
            <option class="normal" value="normal">Normal</option>
            <option class="fire" value="fire">Fire</option>
            <option class="water" value="water">Water</option>
            <option class="electric" value="electric">Electric</option>
            <option class="grass" value="grass">Grass</option>
            <option class="ice" value="ice">Ice</option>
            <option class="fighting" value="fighting">Fighting</option>
            <option class="poison" value="poison">Poison</option>
            <option class="ground" value="ground">Ground</option>
            <option class="flying" value="flying">Flying</option>
            <option class="psychic" value="psychic">Psychic</option>
            <option class="bug" value="bug">Bug</option>
            <option class="rock" value="rock">Rock</option>
            <option class="ghost" value="ghost">Ghost</option>
            <option class="dragon" value="dragon">Dragon</option>
            <option class="dark" value="dark">Dark</option>
            <option class="steel" value="steel">Steel</option>
            <option class="fairy" value="fairy">Fairy</option>
          </select>
          <select class="select-style form-select" name="pokemon-type" id="pokemon-type" v-model="secondTypeChosen"
            v-if="pokemonTypes.length === 2">
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
      <div class="play-again mb-3" v-if="answerDone">
        <button class="btn btn-secondary" @click="pageReload()">Play
          Again</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
* {
  /* font-family: "Lato", serif;
  font-weight: 400;
  font-style: normal; */
}

.normal {
  background-color: #A8A878;
}

.fire {
  background-color: #F08030;
}

.water {
  background-color: #6890F0;
}

.electric {
  background-color: #F8D030;
}

.grass {
  background-color: #78C850;
}

.ice {
  background-color: #98D8D8;
}

.fighting {
  background-color: #C03028;
}

.poison {
  background-color: #A040A0;
}

.ground {
  background-color: #E0C068;
}

.flying {
  background-color: #A890F0;
}

.psychic {
  background-color: #F85888;
}

.bug {
  background-color: #A8B820;
}

.rock {
  background-color: #B8A038;
}

.ghost {
  background-color: #705898;
}

.dragon {
  background-color: #7038F8;
}

.dark {
  background-color: #705848;
}

.steel {
  background-color: #B8B8D0;
}

.fairy {
  background-color: #EE99AC;
}
</style>