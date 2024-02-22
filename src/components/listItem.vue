<template>
    <div>
        <h1 id="pokeName">#{{ id }} - {{ pokemonName }}</h1>
        <img :src="IMG" alt="Front sprite for {{ pokemonName }}">
        <div id="types" v-if="pokeTypes">
            <Type v-for="x in pokeTypes" :type-name="x.type.name"/>
        </div>
    </div>
</template>
<script>
import Type from './type.vue'
export default{
    props:['pokemonName','pokemonUrl','pokemonIndex'],
    data(){
        return {
            sprite:'',IMG:'',id:'',pokeTypes:[]
        }
    },
    methods:{
        async getPokemonInfos(){
            const result = await fetch(this.pokemonUrl);
            this.infos = await result.json();
            this.IMG = this.infos.sprites.front_default;
            this.id = this.infos.id
            this.pokeTypes = this.infos.types;
        }
    },
    created(){
        this.getPokemonInfos();
    },
    components:{
        Type
    }
}
</script>
<style scoped>
div{width: 30%;max-width: 20vh;height: 120px;display: flex;flex-direction: column;justify-content: space-between;align-items: center;
&:hover img{filter: drop-shadow(0 0 0.75rem rgb(57, 20, 220));}}
h1{width: 100%;height: 2em;text-align: center;text-transform: capitalize;}
#types{display: flex;flex-direction: row;justify-content: end;transform: translateX(50%);}
</style>