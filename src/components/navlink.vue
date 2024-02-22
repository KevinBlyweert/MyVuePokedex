<template>
    <a href="" @click.prevent="">{{itemName}}</a>
</template>
<script>
export default{
    props: ['itemName']
}
</script>
<style scoped>
a{font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;text-decoration: none;}
a:visited{color: var(--bgcolor);}
</style>