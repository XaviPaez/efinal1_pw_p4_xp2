<template>
  <CasinoPage />
</template>

<script>
import CasinoPage from "./modules/casino/pages/CasinoPage.vue";

export default {
  name: "App",

  components: {
    CasinoPage,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;

  -webkit-font-smoothing: antialiased;

  -moz-osx-font-smoothing: grayscale;

  text-align: center;

  color: #2c3e50;

  margin-top: 60px;
}
</style>