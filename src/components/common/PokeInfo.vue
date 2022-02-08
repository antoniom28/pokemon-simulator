<template>
    <div class="status-poke" :class="getClass">
      <div class="info" :class="getClass">
        <div class="name">
            <span>{{ poke[indexPoke].name }}</span>
            <span>{{ poke[indexPoke].gender }}</span>
        </div>
        <span>Lv{{ poke[indexPoke].lv }}</span>
      </div>
      <div class="hp-bar">
        <div class="bar">
          <span>HP</span>
          <div class="total-hp"></div> <!--barra verde-->
        </div>
      </div>
      <div class="hp">
        {{ poke[indexPoke].hp }} /
        {{ poke[indexPoke].maxHp }}
      </div>
    </div>
</template>

<script>
export default {
    name: "PokeInfo",
    data(){
        return{}
    },
    props: {
        indexPoke: Number,
        poke: Array,
        getClass: String,
    },
    methods: {},
    computed: {
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
.status-poke {
  height: 120px;
  width: 400px;
  border-top-left-radius: 20px;
  background-color: $bg_main_color;
  position: absolute;
  top: 0;
  left: 400px;

  &.left{
    left: unset;
    right: 400px;
    border-top-left-radius: unset;
    border-top-right-radius: 20px;
  }

  span {
    position: static;
  }

  .info {
    height: 40%;
    width: 100%;
    border-top-left-radius: 20px;
    display: flex;
    justify-content: space-between;
    padding: 0 25px;
    align-items: center;
    background-color: $bg_2_color;

    &.left{
        border-top-left-radius: unset;
        border-top-right-radius: 20px;
    }

    .name{
        min-width: 200px;

        & *{
            margin-right: 20px;
        }
    }
  }

  .bar {
    width: 70%;
    margin: 0 25%;
    background-color: rgb(46, 46, 46);
    color: orange;
    padding: 4px;
    display: flex;
    justify-content: space-between;
    border-radius: 20px;

    .total-hp {
      height: 20px;
      display: inline-block;
      width: 88%;
      border-radius: 15px;
      background-color: green;
    }
  }

  .hp {
    background-color: rgb(226, 226, 226);
    display: inline-block;
    margin-left: 230px;
    padding-right: 15px;
    width: 130px;
    text-align: end;
  }
}
</style>