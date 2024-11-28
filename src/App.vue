<script>
import AppHeader from './components/AppHeader.vue';
import MainCard from './components/MainCard.vue';

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
  <div class="full-page">
    <div class="container mt-4 card-general">
      <AppHeader />
      <MainCard />
    </div>
  </div>
</template>

<style lang="scss">
@use "./style/general.scss" as *;

*:not(.full-page *) {
  background-image: url('./assets/247919.jpg');
  background-size: cover;
  background-position: bottom;
}

.card-general {
  border-radius: 20px;
  -webkit-box-shadow: 8px 0px 0px 0px #DCD0C0, 0px 8px 0px 0px #B1938B, -8px 0px 0px 0px #4E4E56, 0px 0px 0px 8px #DA635D, 5px 5px 15px 5px rgba(0, 0, 0, 0);
  box-shadow: 8px 0px 0px 0px #375DA9, 0px 8px 0px 0px #C92721, -8px 0px 0px 0px #FFCC01, 0px 0px 0px 8px #555557, 5px 5px 15px 5px rgba(0, 0, 0, 0);
  background-color: white;
}
</style>
