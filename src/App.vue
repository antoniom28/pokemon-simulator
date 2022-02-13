<template>
  <div id="app" :class="{'in-battle' : startBattle}">
    <div class="first-container">
      <MainBattle v-if="startBattle" @endBattle="startBattle = false"/>
      <Main v-else @pokeFinded="startBattle = true"/>
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
    };
  },
  created: function(){
    /*setTimeout(() => {
      this.startBattle = true;
    }, 2000);*/
  },
  methods: {
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
