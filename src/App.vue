<script>
// import MainApp from "./components/MainApp.vue";
import AppHeader from "./components/AppHeader.vue";

export default {
  components: {
    AppHeader,
  },
};
</script>

<template>

  <!-- <h1>FrontEnd</h1> -->

  <!-- <MainApp /> -->

  <AppHeader />

  <router-view></router-view>
  
</template>

<style lang="scss">
@use "./styles/general.scss";
</style>
