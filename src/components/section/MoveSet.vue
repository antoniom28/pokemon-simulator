<template>
    <div class="menu">
        <div class="move-set">
            <span @click="turnBack()" class="turn-back">BACK</span>
            <ul>
                <li v-for="(move,index) in userPokemon.moveSet" :key="index" class="move">
                    <span @mouseenter="getMoveInfo(index)" @click="getMove(move,index)">
                        {{move.name}}
                    </span>
                </li>
            </ul>
        </div>

        <div v-if="moveInfo >= 0" class="move-info">
            <div class="move-pp">
                <p>PP</p>
                <p> {{userPokemon.moveSet[moveInfo].pp}} / {{userPokemon.moveSet[moveInfo].totpp}} </p>
            </div>
            <div class="move-type">
                <p> {{userPokemon.moveSet[moveInfo].type}} </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "MoveSet",
    data(){
        return{
            moveInfo: -1,
        }
    },
    methods: {
        getMove(move,index){
            if(index != -1)
                move.pp--;
            console.log(move);
            //this.$emit('',index);
        },
        turnBack(){
            this.$emit('turnBack');
        },
        getMoveInfo(index){
            this.moveInfo = index;
        },
    },
    props: {
        userPokemon: Object,
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
.turn-back{
    cursor: pointer;
    position: absolute;
    top: 0;
    left: 0;
}

.move-set{
    width: 70%;
    height: 100%;
    background-color: skyblue;
    border: 3px double black;
    position: relative;

    ul{
        width: 100%;
        height: 100%;
        display: flex;
        flex-wrap: wrap;

        li{
            width: 50%;
            display: flex;
            justify-content: center;
            align-items: center;

            span{
                cursor: pointer;
            }

            & span:hover::before{
                content:" > ";
            }
        }
    }
}

.move-info{
        width: 30%;
        height: 100%;
        padding: 10px;
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