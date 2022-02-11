<template>
    <div class="menu">
        <ul>
            <li 
                v-for="(poke,index) in allPokemon"
                :key="index"
            >
                <span 
                    :class="{'fainted' : poke.hp == 0}"
                    @click="getPokemon(index)"
                >
                    {{poke.name}}
                </span>
            </li>
        </ul>

        <div v-if="selectedPoke!=null" class="confirm">
            <span> 
                vuoi mandare in campo <br>
                {{selectedPoke}} ?
            </span>
            <div class="confirm-button">
                <span @click="changePoke" > SI </span>
                <span @click="selectedPoke=null" > NO </span>
            </div>
        </div>
        <div v-else class="confirm">
            <div v-if="indexActualPoke >=0" class="turn-back" @click="turnBack" >BACK</div>
            <div v-else>SCEGLI UN <br> POKèMON</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "pokeList",
    data(){
        return{
            selectedPoke: null,
            indexSelectedPoke: null,
        }
    },
    props: {
        allPokemon: Array,
        indexActualPoke: Number,
        allUserFaint: Array,
    },
    methods: {
        getPokemon(index){
            for(let i=0; i<this.allUserFaint.length; i++){
                if(this.allUserFaint[i] == this.allPokemon[index].name)
                    return;
            }
            this.selectedPoke = this.allPokemon[index].name;
            this.indexSelectedPoke = index;
            console.log('pokemon :',index);
            //emit
        },
        changePoke(){
            this.$emit('changePoke',this.selectedPoke,this.indexSelectedPoke);
            this.turnBack();
        },
        turnBack(){
            this.$emit('turnBack');
        }
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
ul{
    width: 100%;
    height: 100%;
    display: flex;
    flex-wrap: wrap;
    width: 70%;
    background-color: white;

    li{
        width: 50%;
        height: 33%;
        display: flex;
        justify-content: center;
        align-items: center;

        span{
            cursor: pointer;
        }
    }
}

.fainted{
    text-decoration: line-through;
    color: red;
    border: 1px solid red;
}

.confirm{
    width: 30%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.confirm-button{
    margin-top: 20px;
    width: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;

    span{
        background-color: rgb(156, 53, 53);
        color: white;
        width: 50px;
        height: 50px;
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
    }
}

.turn-back{
        cursor: pointer;
        background-color: $bg_3_color;
        color: white;
        padding: 50px;
}
</style>