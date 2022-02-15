<template>
    <div class="fill-block">
        <div class="div-block" :style="{width: `${grassW}px`}" >
            <img src="../../assets/img/block-elem/tree.png" alt="">
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
    },
    methods: {},
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
.fill-block{

    img{
    width: 100%;
    z-index: 9999;
    position: relative;
}
}


</style>