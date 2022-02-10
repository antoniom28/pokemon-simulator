<template>
    <main class="container">
        <div class="enemy-field">
            <Field 
                get-class="right enemy"
                :indexActualEnemyPoke="indexActualEnemyPoke"
                :enemyPokemon="enemyPokemon"
                :enemySendAttack="enemySendAttack"
                :enemyGetDamage="enemyGetDamage"
            />
        </div>

        <div class="user-field">
            <Field 
                get-class="left user"
                :indexActualUserPoke="indexActualUserPoke"
                :userPokemon="userPokemon"
                :userSendAttack="userSendAttack"
                :userGetDamage="userGetDamage"
                :ball="ball"
            />

            <div class="menu">
                <Menu 
                    @getMove="getMove"
                    @changePoke="changePokemon"
                    @changePokeInBattle="changePokemonInBattle"
                    :userPokemon="userPokemon"
                    :enemyPokemon="enemyPokemon"
                    :indexActualEnemyPoke="indexActualEnemyPoke"
                />
            </div>
        </div>
    </main>
</template>

<script>
import Field from '../section/Field.vue'
import Menu from '../section/Menu.vue'
import pokeFile from '../../assets/data/pokeFile.json'

export default {
    name: 'Main',
    data(){
        return{
            userPokemon: pokeFile.pokemon,
            enemyPokemon: pokeFile.enemypokemon,
            indexActualUserPoke: -1,
            indexActualEnemyPoke: 0,
            ball: false,
            actualUserMove: -1,
            actualEnemyMove: -1,
            userSendAttack: false,
            enemySendAttack: false,
            enemyGetDamage: false,
            userGetDamage: false,
        }
    },
    methods: {
       getMove(who){
           if(who == 'user')
            this.userSendAttack = true;
           else
            this.enemySendAttack = true;

           if(who == 'user')
                setTimeout(() => {
                    this.enemyGetDamage = true;
                    setTimeout(() => {
                        this.enemyGetDamage = false;
                    }, 500);
                }, 500);
            else
              setTimeout(() => {
                    this.userGetDamage = true;
                    setTimeout(() => {
                        this.userGetDamage = false;
                    }, 500);
                }, 500);


           setTimeout(() => {
               if(who == 'user')
                this.userSendAttack = false;
                else
                this.enemySendAttack = false;
           }, 1000);

           setTimeout(() => {
               if(who == 'user')
                this.enemySendAttack = true;
                else
                this.userSendAttack = true;

                if(who == 'user')
               setTimeout(() => {
               this.userGetDamage = true;
                    setTimeout(() => {
                        this.userGetDamage = false;
                    }, 500);
                }, 500);
                else
                setTimeout(() => {
               this.enemyGetDamage = true;
                    setTimeout(() => {
                        this.enemyGetDamage = false;
                    }, 500);
                }, 500);

               setTimeout(() => {
                   if(who == 'user')
                    this.enemySendAttack = false;
                    else
                    this.userSendAttack = false;
               }, 1000);
           }, 2000);
       },
       changeEnemyPokemon(){
           this.indexActualEnemyPoke++;
       },
       changePokemon(index){
                console.log('change poke in menu',index);
                this.ball=true;
                this.indexActualUserPoke = -1;
                setTimeout(() => {
                    this.indexActualUserPoke = index;
                    this.ball=false;
                }, 1700);
       },
       changePokemonInBattle(index){
                this.enemySendAttack = true;

                setTimeout(() => {
               this.userGetDamage = true;
                    setTimeout(() => {
                        this.userGetDamage = false;
                    }, 500);
                }, 500);

                setTimeout(() => {
                    this.enemySendAttack = false;
                }, 1000);

                setTimeout(() => {
                    this.changePokemon(index);
                }, 2000);
       },
    },
    props: {
    },
    components: {
        Field,
        Menu,
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

.enemy-field, .user-field{
    height: 50%;
    background-color: rgb(173, 255, 173);
    position: relative;
}
.menu{
    width: 100%;
    height: 150px;
    background-color: rgb(211, 211, 211);
    position: absolute;
    bottom: 0;
    left: 0;
}
</style>