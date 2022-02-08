<template>
    <main class="container">
        <div class="enemy-field">
            <Field 
                get-class="right enemy"
                :indexActualEnemyPoke="indexActualEnemyPoke"
                :enemyPokemon="enemyPokemon"
                :enemySendAttack="enemySendAttack"
            />
        </div>

        <div class="user-field">
            <Field 
                get-class="left user"
                :indexActualUserPoke="indexActualUserPoke"
                :userPokemon="userPokemon"
                :userSendAttack="userSendAttack"
                :ball="ball"
            />

            <div class="menu">
                <Menu 
                    @getMove="getMove"
                    @changePoke="changePokemon"
                    :userPokemon="userPokemon"
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
    methods: {
       getMove(index){
           this.actualUserMove = index;
           this.userSendAttack = true;
           setTimeout(() => {
            let pokeDmg = this.userPokemon[this.indexActualUserPoke].moveSet[this.actualUserMove].damage;
            this.enemyPokemon[this.indexActualEnemyPoke].hp -= pokeDmg;
            this.userSendAttack = false;
            this.actualUserMove = -1;
            if(this.enemyPokemon[this.indexActualEnemyPoke].hp <= 0){
                    this.enemyPokemon[this.indexActualEnemyPoke].hp = 0;
                setTimeout(() => {
                    this.changeEnemyPokemon();
                }, 3000);
            } else
                setTimeout(() => {
                    this.getEnemyMove();
                }, 1000);
           }, 1000);
       },
       getEnemyMove(){
           this.actualEnemyMove = Math.floor(Math.random()*4);
           this.enemySendAttack = true;
           setTimeout(() => {
            this.userPokemon[this.indexActualUserPoke].hp -= 
            this.enemyPokemon[this.indexActualEnemyPoke].moveSet[this.actualEnemyMove].damage;
            this.enemySendAttack = false;
            this.actualEnemyMove = 0;
           }, 1000);
       },
       changeEnemyPokemon(){
           this.indexActualEnemyPoke++;
       },
       changePokemon(index){
           let time;
           if(this.indexActualUserPoke >= 0){
            this.getEnemyMove();
            time = 2500;
        } else
            time = 0;
           setTimeout(() => {
                console.log('change poke in menu',index);
                this.ball=true;
                this.indexActualUserPoke = -1;
                setTimeout(() => {
                    this.indexActualUserPoke = index;
                    this.ball=false;
                }, 1700);
           }, time);
       },
    },
    props: {
    },
    components: {
        Field,
        Menu,
    },
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
        }
    }
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