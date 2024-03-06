<template>
    <div id="title">
        <img src="./icons/icon.png" alt="icon" >
        <a href="/">My VueJS Pokedex</a>
    </div>
</template>
<script>

</script>
<style scoped>
#title{display: flex;flex-direction: row;gap: 15px;padding: 15px;align-items: center;}
a{color:black;font-size: 2em;text-decoration: none;font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;color: var(--bgcolor);}
img{width: 45px;height: auto; &:hover{animation: rotate .5s linear infinite;}}
@keyframes rotate{from{transform: rotate(0deg);}to{transform: rotate(360deg);}}
</style>