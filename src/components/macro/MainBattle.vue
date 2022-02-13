<template>
    <main class="container">
        <div class="enemy-field">
            <Field 
                get-class="right enemy"
                :indexActualEnemyPoke="indexActualEnemyPoke"
                :enemyPokemon="enemyPokemon"
                :enemySendAttack="enemySendAttack"
                :specialEnemyMove="specialEnemyMove"
                :enemySpecialName="enemySpecialName"
                :userSpecialName="userSpecialName"
                :enemyGetDamage="enemyGetDamage"
                :enemyBall="enemyBall"
                :spawnField="spawnField"
            />
        </div>

        <div class="user-field">
            <Field 
                get-class="left user"
                :indexActualUserPoke="indexActualUserPoke"
                :userPokemon="userPokemon"
                :userSendAttack="userSendAttack"
                :userSpecialMove="userSpecialMove"
                :userSpecialName="userSpecialName"
                :enemySpecialName="enemySpecialName"
                :userGetDamage="userGetDamage"
                :ball="ball"
                :spawnField="spawnField"
            />

            <div class="menu">
                <Menu 
                    @runAway="runAway"
                    @getMove="getMove"
                    @changePoke="changePokemon"
                    @changePokeInBattle="changePokemonInBattle"
                    :userPokemon="userPokemon"
                    :enemyPokemon="enemyPokemon"
                    :indexActualEnemyPoke="indexActualEnemyPoke"
                    :noClick="noClick"
                    :userPokeFaint="userPokeFaint"
                    :allUserFaint="allUserFaint"
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
    name: 'MainBattle',
    data(){
        return{
            spawnField: true,
            userPokemon: pokeFile.pokemon,
            enemyPokemon: pokeFile.enemypokemon,
            indexActualUserPoke: -1,
            indexActualEnemyPoke: 0,
            indexNextEnemyPoke: 1,
            ball: false,
            enemyBall: false,
            actualUserMove: -1,
            actualEnemyMove: -1,
            userSendAttack: false,
            userSpecialMove: false,
            userSpecialName: "",
            enemySendAttack: false,
            specialEnemyMove: false,
            enemySpecialName: "",
            enemyGetDamage: false,
            userGetDamage: false,
            noClick: true,
            userPokeFaint: false,
            allUserFaint: [],
            allEnemyFaint: [],
        }
    },
    created: function(){
        for(let i=0; i<this.userPokemon.length; i++){
            if(this.userPokemon[i].hp == 0)
                this.allUserFaint.push(this.userPokemon[i].name);
        }

        console.log(this.enemyPokemon.length);
        let random = Math.floor(Math.random()*this.enemyPokemon.length);
        this.indexActualEnemyPoke = random;
        this.enemyPokemon[this.indexActualEnemyPoke].hp = this.enemyPokemon[this.indexActualEnemyPoke].maxHp;
        setTimeout(() => {
            this.spawnField = false;
            this.noClick = false;
        }, 2000);
    },
    methods: {
        runAway(){
            setTimeout(() => {
                this.$emit('endBattle');
            }, 1000);
        },
        controlEnemyHp(){
         let faint = this.enemyPokemon[this.indexActualEnemyPoke].hp;
         console.log('is enemy faint?',faint);
             if(faint == 0){
             setTimeout(() => {
                 this.indexActualEnemyPoke = -1;
                 setTimeout(() => {
                     this.$emit('endBattle');
                 }, 1000);
             }, 1700);
             //this.changeEnemyPokemon();
             return true;
             }
            return false;
        },
        controlUserHp(){
         let faint = this.userPokemon[this.indexActualUserPoke].hp;
         console.log('is user faint?',faint);
             if(faint == 0){
             this.allUserFaint.push(this.userPokemon[this.indexActualUserPoke].name);
             console.log(this.allUserFaint);
             this.changeUserPokemon();
             return true;
             }
            return false;
        },
       getMove(who,userMove, enemyMove){
           console.log(userMove,enemyMove);
           if(who == 'user'){
                this.getUserMove(userMove, enemyMove);
                setTimeout(() => {      
                    if(this.controlEnemyHp())
                        return;
                    this.getEnemyMove(userMove, enemyMove);
                    setTimeout(() => {
                        if(this.controlUserHp())
                        return;
                    }, 2000);
                }, 2000);

           } else{
                this.getEnemyMove(userMove, enemyMove);
                setTimeout(() => {
                    if(this.controlUserHp())
                        return
                    this.getUserMove(userMove, enemyMove);
                          
                    setTimeout(() => {
                        if(this.controlEnemyHp())
                        return;
                    }, 2000);

                }, 2000);
           }
       },
       getEnemyMove(userMove, enemyMove){
        if(enemyMove == null){
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
        } else {
            this.specialEnemyMove = true;
            setTimeout(() => {
                this.userGetDamage = true;
                setTimeout(() => {
                    this.userGetDamage = false;
                }, 300);
            }, 1000);
            this.enemySpecialName = enemyMove;
            setTimeout(() => {
            this.specialEnemyMove = false;
            this.enemySpecialName = "";
            }, 1000);
        }
       },
       getUserMove(userMove, enemyMove){
        if(userMove == null){
            this.userSendAttack = true;
            setTimeout(() => {
                this.enemyGetDamage = true;
                setTimeout(() => {
                    this.enemyGetDamage = false;
                }, 500);
            }, 500);

            setTimeout(() => {
                this.userSendAttack = false;
            }, 1000);
        } else{
            this.userSpecialMove = true;
            setTimeout(() => {
                this.enemyGetDamage = true;
                setTimeout(() => {
                    this.enemyGetDamage = false;
                }, 300);
            }, 1000);
            this.userSpecialName = userMove;
            setTimeout(() => {
                this.userSpecialMove = false;
                this.userSpecialName = "";
            }, 1000);
        }
       },
       changeEnemyPokemon(){
           setTimeout(() => {
               this.indexActualEnemyPoke = -1;
                this.enemyBall = true;
                    this.noClick = true;
                    setTimeout(() => {
                            this.indexActualEnemyPoke = this.indexNextEnemyPoke;
                            this.indexNextEnemyPoke++;
                            this.enemyBall=false;
                            this.noClick = false;
                        }, 1700);
           }, 1500);
       },
       changeUserPokemon(){
           setTimeout(() => {
               this.userPokeFaint = true;
               this.indexActualUserPoke = -1;
               setTimeout(() => {
                   this.userPokeFaint = false;
               }, 100);
           }, 1500);
       },
       changePokemon(index){
                console.log('change poke in menu',index);
                this.ball=true;
                this.indexActualUserPoke = -1;
                this.noClick = true;
                setTimeout(() => {
                    this.indexActualUserPoke = index;
                    this.ball=false;
                    this.noClick = false;

                    setTimeout(() => {
                        let hp = document.querySelectorAll('.total-hp')[1];
                    let barDmg  = document.querySelectorAll('.loss-hp')[1];
                    let dmg = this.userPokemon[this.indexActualUserPoke].maxHp - this.userPokemon[this.indexActualUserPoke].hp;
                    let diff = Math.floor((dmg*100) / this.userPokemon[this.indexActualUserPoke].maxHp);
                    if(diff == 100){
                            hp.style.width = `100%`;
                            barDmg.style.width = `0%`;
                    } 
                    hp.style.width = `${100 - diff}%`;
                    barDmg.style.width = `${diff}%`;
                    }, 100);

                }, 1700);
       },
       changePokemonInBattle(index){
                this.getEnemyMove();
                setTimeout(() => {
                    let hp = document.querySelectorAll('.total-hp')[1];
                    let barDmg  = document.querySelectorAll('.loss-hp')[1];
                    let dmg = this.userPokemon[this.indexActualUserPoke].maxHp - this.userPokemon[this.indexActualUserPoke].hp;
                    let diff = Math.floor((dmg*100) / this.userPokemon[this.indexActualUserPoke].maxHp);
                    if(diff == 100){
                            hp.style.width = `100%`;
                            barDmg.style.width = `0%`;
                    } 
                    hp.style.width = `${100 - diff}%`;
                    barDmg.style.width = `${diff}%`;
                }, 1501);
                this.noClick = true;
                setTimeout(() => {
                    this.changePokemon(index);
                }, 3000);
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
    z-index: 9999;
    bottom: 0;
    left: 0;
}
</style>