<template>
  <div id="app">
    
    <Creator msg="Créez vos équipes !"/>
  </div>
</template>

<script>
import Creator from './components/Creator.vue'


export default {
  name: 'App',
  components: {
    Creator
  }
}
</script>

<style>
*{
  margin: 0;
  padding:0;
  box-sizing: border-box;
  overflow: hidden;
}
body{
  height: 100vh;
}
#app {
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100vw;
  height: 100%;
 /* background: linear-gradient(90deg, rgba(34,11,70,1) 0%, rgba(102,52,163,0.9780287114845938) 46%, rgba(221,178,251,1) 100%); */
 background: rgba(34,11,70,1) ;
 
}

</style>
