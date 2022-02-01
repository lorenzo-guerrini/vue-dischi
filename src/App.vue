<template>
  <div id="app">
    <Header />
    <Main />
  </div>
</template>

<script>
import Header from "./components/macro/Header.vue"
import Main from "./components/macro/Main.vue"

export default {
  name: "App",
  components: {
    Header,
    Main
  },
};
</script>

<style lang="scss">
@import "./assets/style/global.scss";

#app {
  min-width: 900px;
}
</style>
