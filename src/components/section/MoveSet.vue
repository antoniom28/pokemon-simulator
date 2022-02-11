<template>
    <div v-if="!moveUserText && !moveEnemyText && !faint" class="menu">
        <div class="move-set">
            <span @click="turnBack()" class="turn-back">BACK</span>
            <ul>
                <li 
                    @click="getMove(move,index)"
                    @mouseenter="getMoveIndex(index)" 
                    v-for="(move,index) in userPokemon.moveSet" 
                    :key="index" class="move"
                    :class="move.color"
                >
                    <span>
                        {{move.name}}
                    </span>
                </li>
            </ul>
        </div>

        <div v-if="moveIndex >= 0" class="move-info">
            <div class="move-pp">
                <p>PP</p>
                <p> {{userPokemon.moveSet[moveIndex].pp}} / {{userPokemon.moveSet[moveIndex].totpp}} </p>
            </div>
            <div class="move-type">
                <p> {{userPokemon.moveSet[moveIndex].type}} </p>
            </div>
        </div>
    </div>

    <div v-else-if="!moveEnemyText && !faint" class="menu">
        <div class="menu-text">
            {{getUserNameText}} Usa {{getUserMoveText}}
        </div>
    </div>

    <div v-else-if="moveEnemyText" class="menu">
        <div class="menu-text">
            {{getEnemyNameText}} Usa {{getEnemyMoveText}}
        </div>
    </div>

   <div v-else class="menu">
        <div class="menu-text">
            {{pokeFainted}} is fainted!!
        </div>
   </div>
</template>

<script>
export default {
    name: "MoveSet",
    data(){
        return{
            moveIndex: -1,
            enemyMoveIndex: -1,
            moveUserText: false,
            moveEnemyText: false,
            faint: false,
            pokeFainted: "",
        }
    },
    computed: {
        getUserNameText(){
            return this.userPokemon.name;
        },
        getUserMoveText(){
            return this.userPokemon.moveSet[this.moveIndex].name;
        },
        getEnemyNameText(){
            return this.enemyPokemon.name;
        },
        getEnemyMoveText(){
            return this.enemyPokemon.moveSet[this.enemyMoveIndex].name;
        },
    },
    methods: {
        getMove(move,index){
            if(index != -1)
                if(move.pp == 0)
                    move.pp = move.pp;
                else
                    move.pp--;
            this.getEnemyMoveIndex();
                if(this.userPokemon.speed >= this.enemyPokemon.speed){
                this.moveUserText = true;
                this.userStart();
            } else{
                this.moveEnemyText = true;
                this.enemyStart();
            }
        },
        userStart(){
            let enemyFaint = 1;
            let userFaint = 1;
            setTimeout(() => {
                this.$emit('getMove','user');
                setTimeout(() => {
                    enemyFaint = this.getEnemyDamage();
                    console.log('enemy hp in moveset',enemyFaint);
                }, 1000);
                setTimeout(() => {
                    this.moveUserText = false;
                    if(enemyFaint == 0){ 
                        this.faint = true;
                        this.pokeFainted = this.enemyPokemon.name;
                        setTimeout(() => {
                            this.turnBack();
                        }, 1500);
                        return;
                    }
                    this.moveEnemyText = true;
                    setTimeout(() => {
                    userFaint = this.getUserDamage();
                    console.log('user hp in moveset',userFaint);
                    }, 1000);
                    setTimeout(() => {
                        this.moveEnemyText = false;
                        if(userFaint == 0){
                        this.faint = true;
                        this.pokeFainted = this.userPokemon.name;
                        setTimeout(() => {
                            this.turnBack();
                        }, 1500);
                        return;
                        }
                        this.turnBack();
                    }, 2000);
                }, 2000);
            }, 1500);
        },
        enemyStart(){
            let enemyFaint = 1;
            let userFaint = 1;
            setTimeout(() => {
                this.$emit('getMove','enemy');
                setTimeout(() => {
                    userFaint = this.getUserDamage();
                    console.log('hp userO in moveset',userFaint);
                }, 1000);
                setTimeout(() => {
                    this.moveEnemyText = false;
                    if(userFaint == 0){
                        this.faint = true;
                        this.pokeFainted = this.userPokemon.name;
                        setTimeout(() => {
                            this.turnBack();
                        }, 1500);
                        return;
                    }
                    this.moveUserText = true;
                    setTimeout(() => {
                    enemyFaint = this.getEnemyDamage();
                    console.log('hp enemy in moveset',enemyFaint);
                    }, 1000);
                    setTimeout(() => {
                        this.moveUserText = false;
                        if(enemyFaint == 0){
                        this.faint = true;
                        this.pokeFainted = this.enemyPokemon.name;
                        setTimeout(() => {
                            this.turnBack();
                        }, 1500);
                        return;
                    }
                    this.turnBack();
                    }, 2000);
                }, 2000);
            }, 1500);
        },
        getEnemyDamage(){
            this.enemyPokemon.hp -= this.userPokemon.moveSet[this.moveIndex].damage;
            if(this.enemyPokemon.hp <= 0)
                this.enemyPokemon.hp = 0;

        let hp = document.querySelectorAll('.total-hp')[0];
        let barDmg  = document.querySelectorAll('.loss-hp')[0];
        let dmg = this.enemyPokemon.maxHp - this.enemyPokemon.hp;
        let diff = Math.floor((dmg*100) / this.enemyPokemon.maxHp);
        if(diff == 100){
            setTimeout(() => {
                hp.style.width = `100%`;
                barDmg.style.width = `0%`;
            }, 2500);
        } 
        hp.style.width = `${100 - diff}%`;
        barDmg.style.width = `${diff}%`;
        return this.enemyPokemon.hp;

        },
        getUserDamage(){
            this.userPokemon.hp -= this.enemyPokemon.moveSet[this.enemyMoveIndex].damage;
            if(this.userPokemon.hp <= 0)
                this.userPokemon.hp = 0;

        let hp = document.querySelectorAll('.total-hp')[1];
        let barDmg  = document.querySelectorAll('.loss-hp')[1];
        console.log('user hp is',hp,barDmg);
        let dmg = this.userPokemon.maxHp - this.userPokemon.hp;
        let diff = Math.floor((dmg*100) / this.userPokemon.maxHp);
        hp.style.width = `${100 - diff}%`;
        barDmg.style.width = `${diff}%`;

            return this.userPokemon.hp;
        },
        turnBack(){
            this.$emit('turnBack');
        },
        getMoveIndex(index){
            this.moveIndex = index;
        },
        getEnemyMoveIndex(){
            let random = Math.floor(Math.random()*4);
            this.enemyMoveIndex = random;
        },
    },
    props: {
        userPokemon: Object,
        enemyPokemon: Object,
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

.menu-text{
    width: 90%;
    margin: 0 auto;
    height: 100%;
    background-color: $bg_2_color;
    padding: 10px;
    box-shadow: 
        inset 0 0 0 6px rgb(107, 107, 107),
        0 0 0 2px yellow,
        0 0 0 4px black ;
}

.turn-back{
    cursor: pointer;
    position: absolute;
    top: 0;
    left: 0;
}

.move-set{
    width: 70%;
    height: 100%;
    background-color: $bg_2_color;
    border: 3px double black;
    position: relative;

    ul{
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: space-between;
        padding: 10px 10px 10px 50px;
        flex-wrap: wrap;

        li{ //devo dargli la classe delle mosse in global
            cursor: pointer;
            width: calc(50% - 50px);
            margin: 7px 20px;
            display: flex;
            border-radius: 7px;
            justify-content: center;
            align-items: center;

            &:hover{
                transform: scale(1.1);
            }
        }
    }
}

.move-info{
        width: 30%;
        height: 100%;
        padding: 10px 30px;
        border: 3px double black;

        div{
            height: 50%;
            display: flex;
            align-items: center;
        }

        div.move-pp{
            justify-content: space-between;
        }
        div.move-type{
            justify-content: center;
        }
}
</style>