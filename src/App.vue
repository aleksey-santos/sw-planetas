<template>
  <div id="app">
    <h1 id="titulo"></h1>
    <Planeta :planeta="planeta"/>
    <div id="container-botao">
      <button @click="planetaAleatorio()">Blow this up</button>
    </div>
  </div>
</template>

<script>
import Planeta from './components/Planeta.vue'
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Planeta
  },
  data(){
    return {
      planeta: null
    }
  },
  methods:{
    randomIntergetTo(max){
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - 1 + 1)) + 1;
    },
    async carregarPlaneta(idPlaneta){
      try{
        let resposta = await axios.get(`https://swapi.co/api/planets/${idPlaneta}`);
        console.log(resposta);
        if(resposta.data){
          this.planeta = resposta.data;
        }
      }catch(error){
        console.log(error);
        alert('Erro ao buscar informações de planeta!');
      }
    },
    async planetaAleatorio(){
      try{
        let retorno = await axios.get('https://swapi.co/api/planets');
        console.log(retorno);
        let numeroPlanetas = retorno.data.count;
        let idPlaneta = this.randomIntergetTo(numeroPlanetas);
        this.carregarPlaneta(idPlaneta)
      }catch(error){
        console.log(error);
        alert('Erro ao acessar api!');
      }
    },
  },
  created(){
    this.planetaAleatorio();
  },
  componets:{
    Planeta,
  }
}
</script>

<style>

</style>
