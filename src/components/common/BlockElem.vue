<template>
    <div class="fill-block">
        <div class="div-block" :style="{width: `${grassW}px` , height: `${grassH}px`} " >
            <img :src="require('../../assets/img/block-elem/' + type)" alt="">
        </div>
    </div>
</template>

<script>
export default {
    name: "BlockElem",
    data(){
        return{}
    },
    props: {
        grassW: Number,
        grassH: Number,
        type: String,
    },
    methods: {},
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
.fill-block{
    //background-color: red;

    img{
    width: 100%;
    z-index: 9999;
    position: relative;
}
}


</style>