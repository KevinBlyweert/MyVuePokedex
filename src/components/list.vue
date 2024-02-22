<template>
    <div v-if="pokemonList" id="list">
        <div id="buttons">
            <button id="previous" @click="getPokemons(previousUrl,offset,limit,false)" v-show="previousUrl">Previous page</button>
            <button id="next" @click="getPokemons(nextUrl,offset,limit,true)" v-show="nextUrl">Next page</button>
        </div>
        <div id="listItem">
            <listItem  v-for="(x,index) in pokemonList" :pokemon-name="x.name" :pokemon-url="x.url"/>
        </div>
        <div id="buttons">
            <button id="previous" @click="getPokemons(previousUrl,offset,limit,false)" v-show="previousUrl">Previous page</button>
            <button id="next" @click="getPokemons(nextUrl,offset,limit,true)" v-show="nextUrl">Next page</button>
        </div>
    </div>
    <p v-else>Loading...</p>
</template>
<script>
import listItem from './listItem.vue'
export default{
    data(){
        return {
            pokemonList:'',
            previousUrl:'',
            nextUrl:'',
            offset:20,limit:20,
        }
    },
    components:{
        listItem
    },
    methods:{
        async getPokemons(url,offset,limit,next) {
            const response = await fetch(`${url}?limit=${limit}&offset=${offset}`)
            const APIres = await response.json()
            this.pokemonList = APIres.results
            this.previousUrl = APIres.previous
            this.offset = next ? this.offset + this.limit : this.offset - this.limit
            this.nextUrl = APIres.next
        }
    },
    created(){
        this.getPokemons('https://pokeapi.co/api/v2/pokemon')
    }
}
</script>
<style scoped>
#list{display: flex;flex-direction: column;justify-content: space-between;}
#listItem{width: 100%;display: flex;flex-direction: row;flex-wrap: wrap;flex-grow: 1;margin-top: 50px;}
#buttons{display: flex;flex-direction: row;gap: 60px;justify-content: center;}
</style>