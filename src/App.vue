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
  html,body,#app,.hello-world{
    height: 100%;
  }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 14px;
  }
  * {
    padding: 0;
    margin: 0;
  }
  a{
    text-decoration: none;
  }
</style>
