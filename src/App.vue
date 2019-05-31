<template>
  <div id="app">
    <h1 id="titulo">Star Wars Planets</h1>
    <transition name="zoom">
    <Planeta :planeta="planeta" v-show="!loading"/>
    </transition>
    <div id="container-botao">
      <button id="btn-next" @click="planetaAleatorio()">Next</button>
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
      planeta: {
        population:'',
        climate:'',
        terrain:'',
        films:[]
      },
      loading:true
    }
  },
  methods:{
    randomIntergetTo(max){
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - 1 + 1)) + 1;
    },
    async carregarPlaneta(idPlaneta){
      this.loading = true;
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
      this.loading = false;
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
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
}

@font-face {
    font-family: StarJedi;
    src: url(assets/fonts/Starjedi.ttf);
 }
@font-face {
    font-family: StarJediHollow;
    src: url(assets/fonts/Starjhol.ttf);
 }

#app{
  font-family: StarJedi,'sans-serif';
  height:100vh;
  background-color:#222;
  color:yellow;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows:1fr 500px 1fr;
  align-items: center;
  justify-content: center;
}
#titulo{
  font-size: 3em;
  text-align: center;
  font-family: StarJediHollow,sans-serif;
}
#container-botao{
  width: 400px;
      margin:auto;

}
#btn-next{
  outline: none;
  border:1px solid transparent;
  width:100%;
  padding:10px 10px;
  font-size: 1.2em;
  background-color:yellow;
  cursor: pointer;
  font-family: StarJedi,sans-serif;
  color: black;
  transition: all 0.3s ease-in-out;
}
#btn-next:hover{
  color:yellow;
  background-color: black;
}
</style>
