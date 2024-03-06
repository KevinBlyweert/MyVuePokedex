<template>
    <div v-if="pokemonList" id="list">
        <div id="buttons">
            <button id="previous" @click="navigate(false)" v-show="previousUrl">&#60;</button>
            <button v-for="x in Math.ceil(count/limit)" :id="'page'+x" @click="changePage(x)" :class="{active : actualPage === x}">{{ x }}</button>
            <button id="next" @click="navigate(true)" v-show="nextUrl">&#62;</button>
        </div>
        <div id="listItem">
            <listItem  v-for="(x,index) in pokemonList" :key="x.id" :pokemon-name="x.name" :pokemon-url="x.url"/>
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
            offset:0,limit:32,count:0,actualPage:1,
        }
    },
    components:{
        listItem
    },
    methods:{
        async getPokemons() {
            this.pokemonList = "";
            const response = await fetch(`${this.url}?limit=${this.limit}&offset=${this.offset}`);
            const APIres = await response.json();
            this.pokemonList = APIres.results;
            this.previousUrl = APIres.previous;
            this.nextUrl = APIres.next;
            this.count = APIres.count;
        },
        navigate(next){
            if (next) {
                this.offset = this.offset + this.limit;
                this.actualPage++;
            } else {
                this.offset = this.offset - this.limit;
                this.actualPage--;
            }
            this.getPokemons();
        },
        changePage(page){this.offset = (page-1) * this.limit;this.actualPage = page;this.getPokemons()}
    },
    created(){
        this.getPokemons()
    }
}
</script>
<style scoped>
#list{display: flex;flex-direction: column;justify-content: space-between;}
#listItem{width: 100%;display: flex;flex-direction: row;flex-wrap: wrap;flex-grow: 1;margin-top: 50px;justify-content: center;gap: 10px;}
#buttons{display: flex;flex-direction: row;gap: 5px;justify-content: center;flex-wrap: wrap;font-size: .5em;}
button{border: none;color: white;background-color: #c6403d;font-weight: bold;font-size: 1.2em;transition: all .2s;border-radius: 5px;cursor:pointer;
    &:hover{background-color:rgba(255,255,255,0.5);color:black;}
    &.active{background-color:rgba(255,255,255,0.3);border: 1px solid black;}}
#loadingText{text-align: center;color: #fff;font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;font-size: large;}
@media (min-width: 760px) {
    #buttons{font-size: .7em;}
}
@media (min-width: 1160px) {
    #buttons{font-size: 1em;}
}
</style>