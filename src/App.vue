<template>
  <HeaderFile />
  <router-view/>
  <FooterFile />
</template>


<script>
import HeaderFile from './components/HeaderFooter/HeaderFile.vue';
import FooterFile from './components/HeaderFooter/FooterFile.vue';
export default {
  name: 'App',
  components: {
    //HelloWorld
    HeaderFile,
    FooterFile,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
  background-color: #f5f5f5;
}
</style>
