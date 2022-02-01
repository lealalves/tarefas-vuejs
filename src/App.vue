<template>
  <Header />
  <router-view/>
  <Footer />
</template>

<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'


export default {
  name: 'App',
  components: {
    Header,
    Footer
  }
}
</script>

<style>
*{
  text-decoration: none;
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
  #container-principal{
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 550px;
    padding: 30px;
    background-color: aliceblue;
  }
</style>
