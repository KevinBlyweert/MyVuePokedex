<template>
    <div id="pokeType" :class="typeName"></div>
</template>
<script>
export default{
    props:['typeName'],
}
</script>
<style scoped>
#pokeType{width: 20px;height: 20px;border-radius: 50%;z-index: 20;}
</style>