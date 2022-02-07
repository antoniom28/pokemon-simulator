<template>
    <div v-if="getClass == 'right'" id="" class="field">
        <!-- <img src="../../assets/img/.png" alt=""> -->
        <span :class="getClass">
            enemy
        </span>
        <div class="field-terrain" :class="getClass">
        </div>
    </div>

    <div v-else id="" class="field">
        <!-- <img src="../../assets/img/.png" alt=""> -->
        <span :class="getClass">
            <img 
                v-if="userPokemon[indexActualUserPoke].thumb != null"
                :src="getThumb" alt=""
            >
            <span v-else>
                {{userPokemon[indexActualUserPoke].name}}
            </span>
        </span>
        <div class="field-terrain" :class="getClass">
        </div>
    </div>
</template>

<script>
export default {
    name: "Field",
    data(){
        return{}
    },
    props: {
        getClass: String,
        indexActualUserPoke: Number ,
        userPokemon: Array ,
    },
    methods: {},
    computed: {
        getThumb(){
            let image = require(`../../assets/img/${this.userPokemon[this.indexActualUserPoke].thumb}`);
            return image;
        },
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
img{
    width: 100px;
}
.field{
    position: relative;
}

.field-terrain{
    width: 400px;
    height: 300px;
    background-color: yellow;
    border-radius: 50%;
    transform: rotateX(65deg);
    position: absolute;
    top: 0;
    left: 0;

    &.right{
        right: 0;
        left: unset;
    }
}
span{    
    position: absolute;
    top: 0;
    left: 170px;
    z-index: 9999;

    &.right{
        left: unset;
        right: 190px;
    }
}
</style>