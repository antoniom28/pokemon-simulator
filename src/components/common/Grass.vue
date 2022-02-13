<template>
    <main class="fill-grass">
        <div class="div-grass" :style="{height: `${grassH}px`, width: `${grassW}px`}" >
            <div 
                v-for="(elem,index) in col*row"
                :key="index"
                class="grass"
            >
            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: "Grass",
    data(){
        return{}
    },
    props: {
        col: Number,
        row: Number,
        grassW: Number,
        grassH: Number,
    },
    methods: {},
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

.div-grass{
    display: flex;
    flex-wrap: wrap;
    background-color: green;
}

.grass{
    width: 20px;
    height: 20px;
    background-image: url(../../assets/img/grass.jpg);
    background-size: contain;
}
</style>