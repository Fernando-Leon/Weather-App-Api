<template>
  <div id="app">
    <hora>
      
    </hora>


  </div>
</template>
<script>
import hora from '../src/components/hora.vue'
import clima from '../src/components/Clima.vue'
export default{
  components:{
    hora,clima
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
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
