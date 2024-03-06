<template>
    <div id="pokemon">
        <h1 id="pokeName">#{{ id }} - {{ pokemonName }}</h1>
        <img :src="IMG" :alt="alt">
        <div id="types" v-if="pokeTypes">
            <Type v-for="x in pokeTypes" :key="x.id" :type-name="x.type.name"/>
        </div>
    </div>
</template>
<script>
import Type from './type.vue'
export default{
    props:['pokemonName','pokemonUrl','pokemonIndex'],
    data(){
        return {
            sprite:'',IMG:'',id:'',pokeTypes:[],alt:''
        }
    },
    methods:{
        async getPokemonInfos(){
            const result = await fetch(this.pokemonUrl);
            this.infos = await result.json();
            this.IMG = this.infos.sprites.front_default;
            this.alt = "Front sprite for "+this.pokemonName.charAt(0).toUpperCase()+this.pokemonName.slice(1);
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
#pokemon{
    position: relative;
    width: 30%;max-width: 20vh;min-width: 10vh; height: 120px;display: flex;flex-direction: column;justify-content: space-between;align-items: center;background-color: rgba(0,0,0,.1);border-radius:20px;
    img{transition:all .3s ease-in-out;height: 100%;}
    &:hover img{
        filter: drop-shadow(0 0 0.75rem rgb(57, 20, 220));
        transform: scale(1.2,1.2);
    }
}
h1{width: 100%;font-size: 1.2em;text-align: center;text-transform: capitalize;}
#types{display: flex;flex-direction: column;justify-content: end;gap:5px;top:50%;transform:translateY(-50%);position: absolute;right: 5px;align-items: end;}
</style>