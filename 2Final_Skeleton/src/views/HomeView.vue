<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/TX.jpg">
    <br>
    <img alt="Vue logo" src="../assets/euskadi-azul.jpg">
    <br>
    <HelloWorld msg="Ongi etorri CIFP Txurdinaga LHII-ko turismo orrira"/>
    <br>
    <h3>Esta pagina utiliza datos abiertos del Gobierno Vasco, OpenData Euskadi, para su desarrollo</h3>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>
