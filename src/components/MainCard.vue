<script>
export default {
  data() {
    return {
      
    }
  }
}
</script>

<template>
  <header>
    <div class="title">
      <h1>Guess The Pokemon</h1>
    </div>
  </header>

  <main>
    <div class="pokemon-to-guess">
      <div class="pokemon-image">
        <img src="https://www.pokemon.com/static-assets/content-assets/cms2/img/pokedex/full/257.png" alt="blaziken">
      </div>
      <div class="pokemon-question">
        <section>
          Which type is this pokemon?
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