<template>
    <div id="open-menu" class="">
       <DoBox 
        v-if="menuOpt != 0 && menuOpt != 2"
        @getButton="getMenuOption"
        :userPokemon="actualPokemon"
        :noClick="noClick"
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
        :allUserFaint="allUserFaint"
        @turnBack="turnBack"
        @changePoke="changePoke"
        v-if="getOpt == 2"
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
        noClick: Boolean,
        userPokeFaint: Boolean,
        allUserFaint: Array,
    },
    computed: {
        getOpt(){
            console.log(this.userPokeFaint,'daidai');
            if(this.userPokeFaint){
                this.menuOpt = 2;
                this.indexActualPoke = -1;
                }
            return this.menuOpt;
        },
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
        getMoveOption(who){
            this.$emit('getMove',who);
        },
        changePoke(name,index){
            console.log('change poke:' ,name,index);
            if(index == this.indexActualPoke)
                return;
            if(this.indexActualPoke >= 0){
                this.$emit('changePokeInBattle',index);
                this.enemyAttack();
                setTimeout(() => {
                    this.indexActualPoke = index;
                }, 4000);
            } else {
                this.indexActualPoke = index;
                this.$emit('changePoke',index);
            }
            
        },
        enemyAttack(){
            let random = Math.floor(Math.random()*4);
                setTimeout(() => {
                    this.getUserDamage(random);
                }, 1500);
        },
        getUserDamage(move){
            this.userPokemon[this.indexActualPoke].hp 
            -= this.enemyPokemon[this.indexActualEnemyPoke].moveSet[move].damage;
            
            if(this.userPokemon[this.indexActualPoke].hp <= 0)
                this.userPokemon[this.indexActualPoke].hp = 0;
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