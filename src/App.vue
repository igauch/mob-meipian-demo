<template>
  <div id="app">
    <HelloWorld class="hello-world"/>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld'

  export default {
    name: 'App',
    components: {
      HelloWorld
    }
  }
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 14px;
  }
  * {
    padding: 0;
    margin: 0;
    outline: none;
  }
  a{
    text-decoration: none;
  }
</style>
