<template>
  <div id="app">  
    <NavBarr/> 
    <Alunos/>
  </div>
</template>

<script>
import Alunos from './components/comp/Alunos.vue'
import NavBarr from "./components/comp/shared/NavBarr";

export default {
  name: 'App',
  components: {
    Alunos,
    NavBarr
  }
}
</script>

<style>
#app {

}
</style>
