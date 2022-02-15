<template>
  <div id="app" :class="{'in-battle' : startBattle}">
    <div class="first-container">
      <MainBattle v-if="startBattle" @endBattle="startBattle = false"/>
      <Main v-else @pokeFinded="start" :prevPgLeft="pgLeft" :prevPgTop="pgTop"/>
    </div>
  </div>
</template>

<script>
import MainBattle from "./components/macro/MainBattle.vue";
import Main from "./components/macro/Main.vue";

export default {
  name: "App",
  data() {
    return {
        startBattle: false,
        pgTop: 0,
        pgLeft: 0,
    };
  },
  methods: {
      start(pgLeft, pgTop){
        console.log(pgLeft,pgTop);
        this.pgLeft = pgLeft;
        this.pgTop = pgTop;
        this.startBattle = true;
      },
    },
  components: {
    MainBattle,
    Main,
  },
};
</script>

<style lang="scss">
@import "./assets/style/globals.scss";

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.in-battle{
   background-color: #8bff8b;
}

.first-container{
    width: 800px;
    overflow: hidden;
    margin: 0 auto;
    height: 640px;
    font-family: $main_font;
    color: $text_color;
}
</style>
