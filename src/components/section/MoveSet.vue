<template>
    <div v-if="!moveUserText && !moveEnemyText" class="menu">
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

    <div v-else-if="!moveEnemyText" class="menu">
        <div class="menu-text">
            {{getUserNameText}} Usa {{getUserMoveText}}
        </div>
    </div>

    <div v-else class="menu">
        <div class="menu-text">
            {{getEnemyNameText}} Usa {{getEnemyMoveText}}
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
            setTimeout(() => {
                this.$emit('getMove','user');
                setTimeout(() => {
                    this.getEnemyDamage();
                }, 1000);
                setTimeout(() => {
                    this.moveUserText = false;
                    this.moveEnemyText = true;
                    setTimeout(() => {
                    this.getUserDamage();
                    }, 1000);
                    setTimeout(() => {
                        this.moveEnemyText = false;
                        this.turnBack();
                    }, 2000);
                }, 2000);
            }, 1500);
        },
        enemyStart(){
            setTimeout(() => {
                this.$emit('getMove','enemy');
                setTimeout(() => {
                    this.getUserDamage();
                }, 1000);
                setTimeout(() => {
                    this.moveUserText = true;
                    this.moveEnemyText = false;
                    setTimeout(() => {
                    this.getEnemyDamage();
                    }, 1000);
                    setTimeout(() => {
                        this.moveUserText = false;
                        this.turnBack();
                    }, 2000);
                }, 2000);
            }, 1500);
        },
        getEnemyDamage(){
            this.enemyPokemon.hp -= this.userPokemon.moveSet[this.moveIndex].damage;
            if(this.enemyPokemon.hp <= 0)
                this.enemyPokemon.hp = 0;
        },
        getUserDamage(){
            this.userPokemon.hp -= this.enemyPokemon.moveSet[this.enemyMoveIndex].damage;
            if(this.userPokemon.hp <= 0)
                this.userPokemon.hp = 0;
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