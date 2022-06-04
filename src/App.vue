<template>
  <div id="app">
    <Carousel @clicked="cliccato" :risposta="rispa" @gozero="zero"/>
    <Domande :domanda="falla" @risposta="risposto"/>
  </div>
</template>

<script>
import Carousel from './components/Macro/Carousel.vue'
import Domande from './components/Macro/Domande.vue'

export default {
  name: 'App',
  data(){
    return{
      falla: '',
      rispa: '',
    }
  },
  components: {
    Carousel,
    Domande,
  },
  methods: {
    zero(value){
      this.rispa = value;
    },
    cliccato(value){
      this.falla = value;
    },
    risposto(value){
      if(value == '1'){
        this.falla = '0';
        this.rispa = '1';
      }
      else{
        this.falla = '0';
        this.rispa = '0';
      }
    },
  }
}
</script>

<style lang="scss">
#app {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  position: relative;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
