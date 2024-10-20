<script>
import axios from "axios";

export default {
  data() {
    return {
      apiCall: 'https://pokeapi.co/api/v2/pokemon/blaziken'
    }
  }, 
  methods: {
    getApi() {
        axios.get(this.apiCall)
            .then((response) => {
                console.log(response.data.forms[0].name)
                return response.data.forms[0].name;
        })
    },
  },
  mounted() {
    
  }
}
</script>

<template>
</template>

<style scoped>
</style>