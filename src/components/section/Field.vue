<template>

  <div v-if="getClass == 'right enemy'" class="field">
    <span :class="getClass"> 
        <img
            :class="getClass"
            v-if="enemyPokemon[indexActualEnemyPoke].thumb != null"
            :src="getEnemyThumb"
        alt=""
      />
    </span>
    <PokeInfo 
        :indexPoke="indexActualEnemyPoke"
        :poke="enemyPokemon"
        getClass="left enemy"
    />
    <div class="field-terrain" :class="getClass"></div>
  </div>

  <div v-else class="field">
    <span :class="getClass">
      <img
        :class="getClass"
        v-if="userPokemon[indexActualUserPoke].thumb != null"
        :src="getThumb"
        alt=""
      />
      <span v-else>
        {{ userPokemon[indexActualUserPoke].name }}
      </span>
    </span>

    <PokeInfo 
        :indexPoke="indexActualUserPoke"
        :poke="userPokemon"
        getClass="right user"
    />

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
  background-color: yellow;
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