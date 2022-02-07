<template>
  <div id="app">
   <!-- <Header /> -->

    <Main />

   <!-- <Footer /> -->
  </div>
</template>

<script>
//import axios from "axios";
import Main from "./components/macro/Main.vue";
import Footer from "./components/macro/Footer.vue";
import Header from "./components/macro/Header.vue";

export default {
  name: "App",
  data() {
    return {
    };
  },
  methods: {
  },
  components: {
    Main,
    Footer,
    Header,
  },
};
</script>

<style lang="scss">
@import "./assets/style/globals.scss";

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-width: 800px;
  height: 654px;
}
</style>
