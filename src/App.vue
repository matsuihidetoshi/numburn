<template>
  <div id="app">    
    <Square msg="Numburn"/>
  </div>
</template>

<script>
  import Square from './components/Square.vue'
  export default {
    name: 'app',
    components: {
      Square
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 30px;
  }
</style>