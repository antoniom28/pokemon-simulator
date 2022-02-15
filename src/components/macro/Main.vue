<template>
    <main id="main-field-no-battle" class="main" :class="pokeFindend">
        <div 
            v-for="(elem,index) in grassElem" 
            :key="'a'+index" 
            :style="{top: `${elem.top}px`, left: `${elem.left}px`}" 
            class="grass-camp"
        >
            <Grass :col="elem.col" :row="elem.row" :grassW="elem.w" :grassH="elem.h" />
        </div>

        <div 
            v-for="(elem,index) in blockObj" 
            :key="'b'+index" 
            :style="{top: `${elem.top}px`, left: `${elem.left}px`}" 
            class="block-camp"
        >
            <BlockElem :grassW="elem.w" :grassH="elem.h" />
        </div>


        <div id="pg" class="temp-pg">
            <img :src="require('../../assets/img/trainer/' + walk)" alt="">
        </div>
    </main>
</template>

<script>
import Grass from "../common/Grass.vue";
import BlockElem from "../common/BlockElem.vue";

export default {
    name: "Main",
    components:{
        Grass,
        BlockElem,
    },
    props: {
        prevPgLeft: Number,
        prevPgTop: Number,
    },
    data(){
        return{
            walk: "bottom_0.png",
            pokeFindend: "",
            prevPgPos: false,
            pgLeft: 0,
            pgTop: 0,
            blockObj: [
                {
                    top: 500,
                    left: 20,
                    w: 100,
                    h: 100,
                    startX: 20 + 20, 
                    endX: 20 + 100 - 40, 
                    startY: 500 + 40, 
                    endY: 500 + 100 - 20,
                },
                {
                    top: 300,
                    left: 260,
                    w: 100,
                    h: 100,
                    startX: 260 + 20, 
                    endX: 260 + 100 - 40, 
                    startY: 300 + 40, 
                    endY: 300 + 100 - 20,
                },
                {
                    top: 300,
                    left: 380,
                    w: 100,
                    h: 100,
                    startX: 380 + 20, 
                    endX: 380 + 100 - 40, 
                    startY: 300 + 40, 
                    endY: 300 + 100 - 20,
                },
                {
                    top: 20,
                    left: 120,
                    w: 100,
                    h: 100,
                    startX: 120 + 20, 
                    endX: 120 + 100 - 40, 
                    startY: 20 + 40, 
                    endY: 20 + 100 - 20,
                },
                
            ],
            grassElem: [
                {   
                    col: 10,
                    row: 6,
                    top: 60,
                    left: 0,
                    w: 20 * 10,
                    h: 20 * 6,
                },
                {   
                    col: 6,
                    row: 7,
                    top: 300,
                    left: 20,
                    w: 20 * 6,
                    h: 20 * 7,
                },
                {   
                    col: 4,
                    row: 4,
                    top: 300,
                    left: 700,
                    w: 20 * 4,
                    h: 20 * 4,
                },
                {   
                    col: 8,
                    row: 2,
                    top: 600,
                    left: 500,
                    w: 20 * 8,
                    h: 20 * 2,
                },
                {   
                    col: 2,
                    row: 2,
                    top: 20,
                    left: 500,
                    w: 20 * 2,
                    h: 20 * 2,
                },
            ]
        }
    },
    mounted: function(){
        console.log(this.prevPgTop, this.prevPgLeft);
        this.pgTop = this.prevPgTop;
        this.pgLeft = this.prevPgLeft;
        let pg = document.getElementById('pg').style;
        pg.top = `${this.pgTop}px`;
        pg.left = `${this.pgLeft}px`;
    },
    created: function(){
    window.addEventListener('keydown',this.grassControl);
    },
    beforeDestroy: function(){
        //window.removeEventListener('keydown',this.grassControl);
    },
    methods:{
        blockElemControl(key){
            for(let i = 0; i<this.blockObj.length; i++){
                if(key == 'w')
                    if(
                        this.pgTop - 20 >= this.blockObj[i].endY
                        && this.pgLeft <= this.blockObj[i].endX
                        && this.pgLeft >= this.blockObj[i].startX
                    )
                        return true;
                if(key == 's')
                    if(
                        this.pgTop + 20 >= this.blockObj[i].startY 
                        && this.pgLeft <= this.blockObj[i].endX
                        && this.pgLeft >= this.blockObj[i].startX
                    )
                        return true;
                if(key == 'a')
                    if(
                        this.pgLeft - 20 <= this.blockObj[i].endX
                        &&this.pgLeft - 20 >= this.blockObj[i].startX
                        &&this.pgTop <= this.blockObj[i].endY
                        &&this.pgTop >= this.blockObj[i].startY
                    )
                        return true;
                if(key == 'd')
                    if(
                        this.pgLeft + 20 >= this.blockObj[i].startX
                        &&this.pgLeft + 20 <= this.blockObj[i].endX
                        &&this.pgTop <= this.blockObj[i].endY
                        &&this.pgTop >= this.blockObj[i].startY
                    )
                        return true;
            }

            return false;
        },
        grassControl(){
        let pg = document.getElementById('pg').style;
        if(event.key == 'w'){
            if(this.pgTop != 0){
                if(this.blockElemControl('w')){
                    this.walk = "top_0.png";
                } else {
                    if(this.walk == "top_2.png")
                        this.walk = "top_1.png";
                    else
                        this.walk = "top_2.png";
                    this.pgTop -=20;
                    this.prevPgPos = true;
                    pg.top = `${this.pgTop}px`;
                }
            } else{
                this.walk = "top_0.png";
            }
        }
        if(event.key == 's'){
            if(this.pgTop != 640 - 40){
                if(this.blockElemControl('s')){
                    this.walk = "bottom_0.png";
                } else {
                    if(this.walk == "bottom_2.png")
                        this.walk = "bottom_1.png";
                    else
                        this.walk = "bottom_2.png";
                    this.pgTop +=20;
                    this.prevPgPos = true;
                    pg.top = `${this.pgTop}px`;
                }
            } else{
                this.walk = "bottom_0.png";
            }
        }
        if(event.key == 'a'){
            if(this.pgLeft != 0){
                if(this.blockElemControl('a')){
                    this.walk = "left_0.png";
                } else {
                    if(this.walk == "left_2.png")
                        this.walk = "left_1.png";
                    else
                        this.walk = "left_2.png";
                    this.pgLeft -=20;
                    this.prevPgPos = true;
                    pg.left = `${this.pgLeft}px`;
                }
            } else{
                this.walk = "left_0.png";
            }
        }
        if(event.key == 'd'){
            if(this.pgLeft != 800 - 20){
                if(this.blockElemControl('d')){
                    this.walk = "right_0.png";
                } else {
                    if(this.walk == "right_2.png")
                        this.walk = "right_1.png";
                    else
                        this.walk = "right_2.png";
                    this.pgLeft +=20;
                    this.prevPgPos = true;
                    pg.left = `${this.pgLeft}px`;
                }
            } else{
                this.walk = "right_0.png";
            }
        }

        for(let i=0; i<this.grassElem.length; i++){
        let startGrassX = this.grassElem[i].left;
        let endGrassX = this.grassElem[i].left + this.grassElem[i].w - 20;
        let startGrassY = this.grassElem[i].top - 20;
        let endGrassY = this.grassElem[i].top + this.grassElem[i].h - 40;
        if((this.pgTop >= startGrassY && this.pgTop <= endGrassY)
         && (this.pgLeft >= startGrassX && this.pgLeft <= endGrassX)
         &&this.prevPgPos == true){
            console.log('è sull erba');
            this.prevPgPos = false;
            let random = Math.floor(Math.random()*21);
            let random2 = Math.floor(Math.random()*21);
            if(random == random2){
                window.removeEventListener('keydown',this.grassControl);
                this.pokeFindend = 'poke-finded';
                setTimeout(() => {
                    console.log('oasso',this.pgLeft, this.pgTop);
                    this.$emit('pokeFinded',this.pgLeft, this.pgTop);
                }, 3499);
                }
            break;
            }
        }
    }
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
.main{
    position: relative;
    background-color: rgb(115, 155, 4);;
}

.grass-camp,.block-camp{
    position: absolute;
}

.ground{
    width: 20px;
    height: 20px;
    box-shadow: 0 0 0 0.5px black;
    background-color: grey;
}

.temp-pg{
    position: absolute;
    top:0;
    left: 0;
    width: 20px;
    height: 20px;
    overflow: hidden;
    transform: scale(1.2) translate(0px , 10px);

    img{
        width: 20px;
    }
}

#main-field-no-battle.poke-finded{
    animation: finded 3s 0.5s linear;
}

@keyframes finded {
    0%{ filter: brightness(0.2); }
    25%{ filter: brightness(1); }
    50%{ filter: brightness(0.2); transform: scale(1) rotate(0deg);}
    100%{
        filter: unset;
        transform: scale(0.01) rotate(360deg);
    }
}
</style>