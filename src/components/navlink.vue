<template>
    <button @click.prevent="emitLink">{{itemName}}</button>
</template>
<script>
export default{
    props: ['itemName'],

    methods:{
        emitLink(){
            this.$emit('emit',this.itemName)
        },
    }
}
</script>
<style scoped>
button{font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;text-decoration: none;color:var(--bgcolor);background-color: #fff;border: none;font-size: 1.2em;}
</style>