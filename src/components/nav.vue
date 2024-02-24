<template>
    <button id="burger" @click="navOpen =! navOpen" v-bind:class="{active : navOpen}">
        <span class="top"></span>
        <span class="middle"></span>
        <span class="bottom"></span>
    </button>
    <nav id="nav" v-bind:class="{open : navOpen}" v-show="navOpen || windowWidth" >
        <Navlink v-for="x in navItems" :item-name="x" />
    </nav>
</template>
<script>
import Navlink from "./navlink.vue";
export default{
    data(){
        return {
            navOpen:false,
            navItems:["Pokemon"],
            windowWidth:window.innerWidth
        }
    },
    components:{
        Navlink
    },
}
</script>
<style scoped>
#nav{
    display: none;
    /* position: absolute;
    display: none;
    height: 0;bottom: 0;
    transition: all .5s;
    padding: 15px;*/
    &.open{
        position: absolute;
        display: flex;
        flex-direction: column;
        top: 50%;
        right: 0;
        padding-top: 52px;
        background-color: #fff;
        width: 100px;height: 90px;
    }
}
#burger{
    display: block;
    width: 25px;
    height: 25px;
    right: 15px;
    background: rgb(255, 255, 255);
    border: none;
    position: absolute;
    z-index: 100;
    appearance: none;
    cursor: pointer;
    outline: none;
    top:50%;
    transform: translateY(-50%);
    span {
        display: block;
        width: 20px;
        height: 2px;
        margin-top: 11px;
        background: rgb(80, 40, 40);
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        transition: all .4s ease;

        &.top {
            transform: translateY(-8px);
        }

        &.bottom {
            transform: translateY(8px);
        }
    }
    &.active{
        .top {
            transform: rotate(-45deg);
        }
        .middle{
            width :0px;
        }
        .bottom {
            transform: rotate(45deg);
        }
    }
}
@media (min-width: 700px) {
  #burger{display:none}
  #nav{display: flex;flex-direction: row;justify-content: end;gap: 50px;align-items: center;padding: 15px;}
}
</style>