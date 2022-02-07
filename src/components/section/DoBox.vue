<template>
    <div class="menu">
        <div class="do-box">
            What will {{userPokemon.name}} do?
        </div>

        <div class="action">
            <ul>
                <li @click="getButton(0)" class="fight">FIGHT</li>
                <li @click="getButton(1)" class="bag">BAG</li>
                <li @click="getButton(2)" class="pokemon">POKèMON</li>
                <li @click="getButton(3)" class="run">RUN</li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: "DoBox",
    data(){
        return{}
    },
    methods: {
        getButton(index){
            console.log(index);
            this.$emit('getButton',index);
        },},
    props: {
        userPokemon: Object,
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

.do-box{
    width: 39%;
    height: 100%;
    background-color: &bg_2_color;
    padding: 10px;
    box-shadow: 
        inset 0 0 0 6px rgb(107, 107, 107),
        0 0 0 2px yellow,
        0 0 0 4px black ;
}

.action{
    width: 59%;
    height: 100%;

    ul{
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;

        li{
            cursor: pointer;
            color: white;
            font-size: 2.3em;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 47%;
            height: 40%;
            margin: 0 5px;
            border-radius: 50px;
            box-shadow: 0 0 0px 2px white, 0 0 0px 6px black;
        }
    }
}

li.fight{
    background-color: #f59191;
    &:hover{
        box-shadow: 0 0 0px 2px white, 0 0 0px 6px red;
    }
}
.bag{
    background-color: #9d7938;
    &:hover{
        box-shadow: 0 0 0px 2px white, 0 0 0px 6px orange;
    }
}
.pokemon{
    background-color: #1d751d;
    &:hover{
        box-shadow: 0 0 0px 2px white, 0 0 0px 6px green;
    }
}
.run{
    background-color: #6262d3;
    &:hover{
        box-shadow: 0 0 0px 2px white, 0 0 0px 6px blue;
    }
}
</style>