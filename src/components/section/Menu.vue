<template>
    <div id="open-menu" class="">
       <DoBox 
        v-if="menuOpt != 0 && menuOpt != 2"
        @getButton="getMenuOption"
        :userPokemon="actualPokemon"
       />

      <MoveSet 
        v-if="menuOpt == 0"
        @getMove="getMoveOption"
        @turnBack="turnBack"
        :userPokemon="actualPokemon"
        :enemyPokemon="actualEnemyPokemon"
      />

      <pokeList 
        :allPokemon="userPokemon"
        :indexActualPoke="indexActualPoke"
        @turnBack="turnBack"
        @changePoke="changePoke"
        v-if="menuOpt == 2"
      />
    </div>
</template>

<script>
import DoBox from '../section/DoBox.vue'
import MoveSet from '../section/MoveSet.vue'
import pokeList from '../section/pokeList.vue'

export default {
    name: "Menu",
    components: {
        DoBox,
        MoveSet,
        pokeList,
    },
    data(){
        return{
            menuOpt: 2,
            indexActualPoke: -1,
        }
    },
    props: {
        userPokemon: Array,
        enemyPokemon: Array,
        indexActualEnemyPoke: Number,
    },
    computed: {
        actualPokemon(){
            return this.userPokemon[this.indexActualPoke];
        },
        actualEnemyPokemon(){
            return this.enemyPokemon[this.indexActualEnemyPoke];
        },
    },
    methods: {
        turnBack(){
            this.menuOpt = -1;
        },
        getMenuOption(index){
            console.log('menu option: ',index);
            this.menuOpt = index;
        },
        getMoveOption(index){
            console.log('move :',index);
            if(index == -1)
                this.menuOpt = index;
            else{
                this.$emit('getMove',index);
            }
        },
        changePoke(name,index){
            console.log('change poke:' ,name,index);
            this.indexActualPoke = index;
            this.$emit('changePoke',index);
        },
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
#open-menu{
    width: 100%;
    height: 100%;
}

.menu{
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 100%;
    padding: 10px;
}

</style>