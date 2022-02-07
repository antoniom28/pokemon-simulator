<template>
    <header class="container">
        <div>
            logo
            <!-- <elemento /> -->
        </div>

        <nav>
            <ul>
                <li
                    v-for="(elem,index) in menuItem"
                    :key="index"
                >
                    {{elem}}
                </li>
            </ul>
        </nav>

    </header>
</template>

<script>
//import elemento from '../section/elemento.vue'

export default {
    name: 'Header',
    components: {
        //elemento
    },
    data(){
        return{
            menuItem: ['elem1','elem2','elem3'],
        }
    },
    props: {},
    methods: {},
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 50px;
    background-color: $bg_color;
    padding: 0 10px;

    ul{
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 300px;

        li{
            cursor: pointer;
            color: $text_color;

            &:hover{
                color:$text_2_color;
            }
        }
    }
}
</style>