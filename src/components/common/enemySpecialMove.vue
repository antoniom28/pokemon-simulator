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

.palla-infuocata{
    position: absolute;
    top: 55px;
    left: -15px;
    transform: scale(0.2) rotate(180deg);
    animation: palla-infuocata 1s linear;

    img{
    width: 100px;
    }
}

@keyframes palla-infuocata {
   0%{
       transform: scale(0.2) rotate(180deg);
        top: 55px;
        left: -15px;
   } 
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
   0%{
        top: 170px;
        left: -396px;
   }
   100%{
        top: 340px;
        left: -396px;
   }
}
</style>