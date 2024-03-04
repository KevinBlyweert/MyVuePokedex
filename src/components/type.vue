<template>
    <div id="pokeType" :class="typeName"><span>{{ typeName }}</span></div>
</template>
<script>
export default{
    props:['typeName'],
}
</script>
<style scoped>
#pokeType{
    width: 20px;height: 20px;border-radius: 50%;z-index: 20;will-change: width;transition: all .3s;color:rgba(255,255,255,0);font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    span{display: none;}
    &:hover{
        width: auto;border-radius: 5px;color:#fff;text-align: center;text-shadow: 0 0 3px #000;padding: 0 5px;
        span{display: inline;}
    }
}
</style>