<template>
    <div class="menu">
        <ul>
            <li 
                v-for="(poke,index) in allPokemon"
                :key="index"
            >
                <span @click="getPokemon(index)">
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
                <span @click="turnBack" > NO </span>
            </div>
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
    },
    methods: {
        getPokemon(index){
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
            this.$emit('turnBack',-1);
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
        background-color: gray;
        color: white;
        width: 50px;
        height: 50px;
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
    }
}
</style>