<template>
    <main class="container">
        <div class="enemy-field">
            <Field />
        </div>
        <div class="user-field">
            <Field />
            <div class="menu">
                <Menu 
                    :userPokemon="userPokemon"
                />
            </div>
        </div>
    </main>
</template>

<script>
import Field from '../section/Field.vue'
import Menu from '../section/Menu.vue'
import userPokemon from '../../assets/data/userPokemon.json'

export default {
    name: 'Main',
    mounted : function(){
        console.log(userPokemon.pokemon);
    },
    props: {
    },
    components: {
        Field,
        Menu,
    },
    data(){
        return{
            userPokemon: userPokemon.pokemon,
            enemyPokemon: ['peppe','francoDino'],
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
.enemy-field, .user-field{
    height: 50vh;
    background-color: rgb(173, 255, 173);
    position: relative;
}
.menu{
    width: 100%;
    height: 150px;
    background-color: rgb(211, 211, 211);
    position: absolute;
    bottom: 0;
    left: 0;
}
</style>