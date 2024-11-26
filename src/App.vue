<script>
import AppHeader from './components/AppHeader.vue';
import MainCard from './components/MainCard.vue';

import axios from 'axios';

export default {
  data() {
    return {

    }
  },
  components: {
    AppHeader,
    MainCard,
  }
}
</script>

<template>
  <div class="container">
    <AppHeader />
    <MainCard />
  </div>
</template>

<style lang="scss">
@use "./style/general.scss" as *;
</style>
