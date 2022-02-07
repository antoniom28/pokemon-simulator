<template>

  <div v-if="getClass == 'right enemy'" class="field">
    <span :class="getClass"> 
        <img
            :class="getClass"
            v-if="indexActualEnemyPoke >= 0"
            :src="getEnemyThumb"
        alt=""
      />
    </span>
    <PokeInfo 
        v-if="indexActualEnemyPoke >= 0"
        :indexPoke="indexActualEnemyPoke"
        :poke="enemyPokemon"
        getClass="left enemy"
    />
    <div class="field-terrain" :class="getClass"></div>
  </div>

  <div v-else class="field"> <!-- LEFT USER -->
    <span :class="getClass">
      <img
        :class="getClass"
        v-if="indexActualUserPoke >= 0"
        :src="getThumb"
        alt=""
      />
    </span>

    <PokeInfo 
        v-if="indexActualUserPoke >= 0"
        :indexPoke="indexActualUserPoke"
        :poke="userPokemon"
        getClass="right user"
    />
    <div v-if="ball" class="ball">
      <img src="../../assets/img/ball.png" alt="">
    </div>

    <div class="field-terrain" :class="getClass"></div>
  </div>
</template>

<script>
import PokeInfo from '../common/PokeInfo.vue'

export default {
  name: "Field",
  components: {
      PokeInfo,
  },
  data() {
    return {};
  },
  props: {
    getClass: String,
    userPokemon: Array,
    indexActualUserPoke: Number,
    enemyPokemon: Array,
    indexActualEnemyPoke: Number,
    ball: Boolean,
  },
  methods: {},
  computed: {
    getThumb() {
      let image = require(`../../assets/img/poke-img/${
        this.userPokemon[this.indexActualUserPoke].thumb
      }`);
      return image;
    },
    getEnemyThumb() {
      let image = require(`../../assets/img/poke-img/${
        this.enemyPokemon[this.indexActualEnemyPoke].thumb
      }`);
      return image;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/style/partials/variables.scss";
.ball{
  position: absolute;
  top: 70px;
  left: -50px;
  animation: throw 1.5s linear forwards; 
  z-index: 9999;
  
  img{
    width: 40px;
  }
}

@keyframes throw {
  0%{
    transform: rotate(0deg);
    top: 70px;
    left: -50px;
  }
  10%{
    transform: rotate(90deg);
    top: 75px;
    left: -27.5px;
  }
  20%{
    transform: rotate(180deg);
    top: 80px;
    left: -5px;
  }
  30%{
    transform: rotate(270deg);
    top: 85px;
    left: 17.5px;
  }
  40%{
    transform: rotate(330deg);
    top: 90px;
    left: 40px;
  }
  50%{
    top: 110px;
    left: 62.5x;
    transform: rotate(360deg);
  }
  55%{
      top: 90px;
      transform: rotate(540deg);
  }
  60%{
    top: 110px;
    transform: rotate(720deg);
    left: 85px;
  }
  70%{
      top: 100px;
      transform: rotate(900deg);
    left: 107.5x;
  }
  80%{
    top: 110px;
    left: 130px;
    transform: rotate(1080deg);
  }
  90%{
    left: 152.5px;
    transform: rotate(1260deg);
  }
  100%{
    transform: rotate(1440deg);
    top: 110px;
    left: 185px;
  }
}


img {
  width: 100px;
}

img.left {
  width: 130px;
}

img.right {
  width: 110px;
}


.field {
  position: relative;
  width: 100%;
  height: 100%;
}

.field-terrain {
  width: 400px;
  height: 300px;
  background-color: $field_color;
  border-radius: 50%;
  transform: rotateX(70deg);
  position: absolute;
  top: 0;
  left: 0;

  &.right {
    right: 0;
    left: unset;
  }
}

span {
  position: absolute;
  bottom: 146px;
  left: 130px;
  z-index: 9999;

  &.right {
    bottom: unset;
    top: 50px;
    left: unset;
    right: 150px;
  }
}
</style>