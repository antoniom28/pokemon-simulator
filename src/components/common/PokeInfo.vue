<template>
    <div class="status-poke">
      <div class="info">
        <div class="name">
            <span>{{ userPokemon[indexActualUserPoke].name }}</span>
            <span>{{ userPokemon[indexActualUserPoke].gender }}</span>
        </div>
        <span>Lv{{ userPokemon[indexActualUserPoke].lv }}</span>
      </div>
      <div class="hp-bar">
        <div class="bar">
          <span>HP</span>
          <div class="total-hp"></div> <!--barra verde-->
        </div>
      </div>
      <div class="hp">
        {{ userPokemon[indexActualUserPoke].hp }} /
        {{ userPokemon[indexActualUserPoke].maxHp }}
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
        indexActualUserPoke: Number,
        userPokemon: Array,
    },
    methods: {},
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
.status-poke {
  height: 120px;
  width: 400px;
  background-color: rgb(196, 196, 196);
  position: absolute;
  top: 0;
  right: 0;

  span {
    position: static;
  }

  .info {
    height: 40%;
    width: 100%;
    display: flex;
    justify-content: space-between;
    padding: 0 25px;
    align-items: center;
    background-color: rgb(226, 226, 226);

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