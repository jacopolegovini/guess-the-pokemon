<script>
import MainCard from './components/MainCard.vue';
import axios from 'axios';

export default {
  data() {
    return {
      
    }
  },
  components: {
    MainCard,
  }
}
</script>

<template>
  <div class="container">
    <MainCard />
  </div>
</template>

<style lang="scss">
@use "./style/general.scss" as *;
</style>
