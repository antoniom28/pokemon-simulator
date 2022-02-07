<template>
    <main class="container">
        <div class="enemy-field">
            <Field 
                get-class="right enemy"
                :indexActualEnemyPoke="indexActualEnemyPoke"
                :enemyPokemon="enemyPokemon"
            />
        </div>

        <div class="user-field">
            <Field 
                get-class="left user"
                :indexActualUserPoke="indexActualUserPoke"
                :userPokemon="userPokemon"
            />

            <div class="menu">
                <Menu 
                    @changePoke="changePokemon"
                    :userPokemon="userPokemon"
                />
            </div>
        </div>
    </main>
</template>

<script>
import Field from '../section/Field.vue'
import Menu from '../section/Menu.vue'
import pokeFile from '../../assets/data/pokeFile.json'

export default {
    name: 'Main',
    methods: {
       changePokemon(index){
           console.log('change poke in menu',index);
           this.indexActualUserPoke = index;
       },
    },
    props: {
    },
    components: {
        Field,
        Menu,
    },
    data(){
        return{
            userPokemon: pokeFile.pokemon,
            enemyPokemon: pokeFile.enemypokemon,
            indexActualUserPoke: 0,
            indexActualEnemyPoke: 1,
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

.enemy-field, .user-field{
    height: 50%;
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