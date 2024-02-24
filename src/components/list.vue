<template>
    <div v-if="pokemonList" id="list">
        <div id="buttons">
            <button id="previous" @click="navigate(false)" v-show="previousUrl">&#60;</button>
            <button id="next" @click="navigate(true)" v-show="nextUrl">&#62;</button>
        </div>
        <div id="listItem">
            <listItem  v-for="(x,index) in pokemonList" :key="x.id" :pokemon-name="x.name" :pokemon-url="x.url"/>
        </div>
        <div id="buttons">
            <button id="previous" @click="navigate(false)" v-show="previousUrl">&#60;</button>
            <button id="next" @click="navigate(true)" v-show="nextUrl">&#62;</button>
        </div>
    </div>
    <p v-else id="loadingText">Loading...</p>
</template>
<script>
import listItem from './listItem.vue'
export default{
    data(){
        return {
            url:'https://pokeapi.co/api/v2/pokemon',
            pokemonList:'',
            previousUrl:'',
            nextUrl:'',
            offset:0,limit:24,
        }
    },
    components:{
        listItem
    },
    methods:{
        async getPokemons() {
            const response = await fetch(`${this.url}?limit=${this.limit}&offset=${this.offset}`)
            const APIres = await response.json()
            this.pokemonList = APIres.results
            this.previousUrl = APIres.previous
            this.nextUrl = APIres.next
        },
        navigate(next){this.offset = next ? this.offset + this.limit : this.offset - this.limit;this.pokemonList = "";this.getPokemons()},
    },
    created(){
        this.getPokemons()
    }
}
</script>
<style scoped>
#list{display: flex;flex-direction: column;justify-content: space-between;}
#listItem{width: 100%;display: flex;flex-direction: row;flex-wrap: wrap;flex-grow: 1;margin-top: 50px;justify-content: center;gap: 10px;}
#buttons{display: flex;flex-direction: row;gap: 60px;justify-content: center;}
button{border: none;color: white;background-color: #c6403d;font-weight: bold;font-size: 1.2em;transition: all .2s;&:hover{background-color:rgba(255,255,255,0.3)}}
#loadingText{text-align: center;color: #fff;font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;font-size: large;}
</style>