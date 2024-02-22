<script setup>
import Header from './components/header.vue'
import Nav from './components/nav.vue'
import List from './components/list.vue'
</script>

<template>
  <header>
    <Header />
    <Nav />
  </header>
  <main>
    <List style="flexGrow:1;paddingTop: 20px;"/>
  </main>
  <footer>
    <div>&copy;Me & Pokémon - 2024</div>
  </footer>
</template>

<style scoped>
header,footer{position: relative; display: flex;flex-direction: row;justify-content: space-between; background-color: #fff;border:15px solid var(--bgcolor);border-radius: 50px;}
Nav{flex-grow: 1;position: relative;}
main{display: flex;flex-direction: column;justify-content: space-between;
select{width: 20vh;align-self:self-end;margin-right: 15px;}}
footer{
  div{height: 45px;width: 100%;text-align: center;font-size: 2em;display: flex;flex-direction: column;justify-content: center;}
}
</style>
