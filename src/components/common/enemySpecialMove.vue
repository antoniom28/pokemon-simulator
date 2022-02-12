<template>

    <div v-if="enemySpecialName == 'palla infuocata'" class="palla-infuocata">
        <img
          class="special"
          src="../../assets/img/move/palla.png"
          alt=""
        />
    </div>

    <div v-else-if="enemySpecialName == 'pietramma'" class="pietramma">
        <img
          class="special"
          src="../../assets/img/move/pietramma.png"
          alt=""
        />
    </div>

    <div v-else-if="enemySpecialName == 'mega salto'" class="mega-salto">
        <div class="special-div"></div>
    </div>

    <div v-else-if="enemySpecialName == 'bomba velenosa'" class="bomba-velenosa">
        <div class="bomba-velenosa-div"></div>
    </div>
</template>

<script>
export default {
    name: "enemySpecialMove",
    data(){
        return{}
    },
    props: {
        enemySpecialName: String,
    },
    methods: {},
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
img{
    width: 60px;
}

.bomba-velenosa{
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: rgb(255, 70, 255);
    position: absolute;
    transform: scale(0.4);
    top: 55px;
    left: -15px;
    animation: bomba-velenosa 1.05s linear;
}

@keyframes bomba-velenosa {
    70%{
        transform: scale(0.4);
        top: 410px;
        left: -365px;
    }
    100%{
        transform: scale(4) rotateX(70deg);
        top: 410px;
        left: -365px;
    }
}

.mega-salto{
    width: 150px;
    height: 150px;
    border-radius: 50%;
    background-color: skyblue;
    position: absolute;
    top: 0px; 
    left: 0px;
    animation: mega-salto 1.05s linear;
}

@keyframes mega-salto {
    100%{
        top: 330px; 
        left: -370px;
    }
}

.palla-infuocata{
    position: absolute;
    top: 55px;
    left: -15px;
    transform: scale(0.2) rotate(180deg);
    animation: palla-infuocata 1.05s linear;

    img{
    width: 100px;
    }
}

@keyframes palla-infuocata {
   30%{
       transform: scale(0.5) rotate(180deg);
   }
   100%{
       transform: scale(1.2) rotate(180deg);
        top: 330px;
        left: -325px;
   }
}

.pietramma{
    position: absolute;
    top: 170px;
    left: -396px;
    transform: scale(2);
    animation: pietramma 1.05s linear;

    img{
    width: 100px;
    }
}

@keyframes pietramma {
   100%{
        top: 340px;
        left: -396px;
   }
}
</style>