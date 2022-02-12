<template>

    <div v-if="userSpecialName == 'palla infuocata'" class="palla-infuocata">
        <img
          class="special"
          src="../../assets/img/move/palla.png"
          alt=""
        />
    </div>

    <div v-else-if="userSpecialName == 'pietramma'" class="pietramma">
        <img
          class="special"
          src="../../assets/img/move/pietramma.png"
          alt=""
        />
    </div>
</template>

<script>
export default {
    name: "specialMove",
    data(){
        return{}
    },
    props: {
        userSpecialName: String,
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
    top: -25px;
    left: 90px;
    transform: scale(0.2);
    animation: palla-infuocata 1s linear;

    img{
    width: 100px;
    }
}

@keyframes palla-infuocata {
   0%{
       transform: scale(0.2);
         top: -25px;
        left: 90px;
   } 
   30%{
       transform: scale(0.5);
   }
   100%{
       transform: scale(1.2);
        top: -290px;
        left: 380px;
   }
}

.pietramma{
    position: absolute;
    top: -475px;
    left: 400px;
    transform: scale(2);
    animation: pietramma 1s linear;

    img{
    width: 100px;
    }
}

@keyframes pietramma {
   0%{
        top: -475px;
        left: 400px;
   }
   100%{
        top: -300px;
        left: 400px;
   }
}
</style>