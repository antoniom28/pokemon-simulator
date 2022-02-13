<template>
    <main id="main-field-no-battle" class="main" :class="pokeFindend">
        <div class="main-field">
          <!--  <div 
                class="ground"
                v-for="(ground,index) in 1320"
                :key="index"
            ></div> -->
        </div>

        <div 
            v-for="(elem,index) in grassElem" 
            :key="index" 
            :style="{top: `${elem.top}px`, left: `${elem.left}px`}" 
            class="grass-camp"
        >
            <Grass :col="elem.col" :row="elem.row" :grassW="elem.w" :grassH="elem.h" />
        </div>


        <div id="pg" class="temp-pg">
            <img :src="require('../../assets/img/trainer/' + walk)" alt="">
        </div>
    </main>
</template>

<script>
import Grass from "../common/Grass.vue";

export default {
    name: "Main",
    components:{
        Grass,
    },
    data(){
        return{
            walk: "bottom_0.png",
            pokeFindend: "",
            pgLeft: 0,
            pgTop: 0,
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
    created: function(){
    window.addEventListener('keydown',this.grassControl);
    },
    beforeDestroy: function(){
        //window.removeEventListener('keydown',this.grassControl);
    },
    props: {},
    methods:{
        grassControl(){
        let pg = document.getElementById('pg').style;
        if(event.key == 'w'){
            if(this.pgTop != 0){
                if(this.walk == "top_2.png")
                    this.walk = "top_1.png";
                else
                    this.walk = "top_2.png";
                this.pgTop -=20;
                pg.top = `${this.pgTop}px`;
            } else{
                this.walk = "top_0.png";
            }
        }
        if(event.key == 's'){
            if(this.pgTop != 640 - 20){
                if(this.walk == "bottom_2.png")
                    this.walk = "bottom_1.png";
                else
                    this.walk = "bottom_2.png";
                this.pgTop +=20;
                pg.top = `${this.pgTop}px`;
            } else{
                this.walk = "bottom_0.png";
            }
        }
        if(event.key == 'a'){
            if(this.pgLeft != 0){
                if(this.walk == "left_2.png")
                    this.walk = "left_1.png";
                else
                    this.walk = "left_2.png";
                this.pgLeft -=20;
                pg.left = `${this.pgLeft}px`;
            } else{
                this.walk = "left_0.png";
            }
        }
        if(event.key == 'd'){
            if(this.pgLeft != 800 - 20){
                if(this.walk == "right_2.png")
                    this.walk = "right_1.png";
                else
                    this.walk = "right_2.png";
                this.pgLeft +=20;
                pg.left = `${this.pgLeft}px`;
            } else{
                this.walk = "right_0.png";
            }
        }

        for(let i=0; i<this.grassElem.length; i++){
        let startGrassX = this.grassElem[i].left;
        let endGrassX = this.grassElem[i].left + this.grassElem[i].w - 20;
        let startGrassY = this.grassElem[i].top;
        let endGrassY = this.grassElem[i].top + this.grassElem[i].h - 20;
        if((this.pgTop >= startGrassY && this.pgTop <= endGrassY)
         && (this.pgLeft >= startGrassX && this.pgLeft <= endGrassX)){
            console.log('è sull erba');
            let random = Math.floor(Math.random()*11);
            console.log(random);
            if(random == 6){
                window.removeEventListener('keydown',this.grassControl);
                this.pokeFindend = 'poke-finded';
                setTimeout(() => {
                    this.$emit('pokeFinded');
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

[class*="grass-camp"]{
    position: absolute;
}

.main-field{
    position: absolute;
    display: flex;
    flex-wrap: wrap;
    top: 0;
    left: 0;
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