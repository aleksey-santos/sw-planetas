<template>
  <div class="planeta">
      <div class="titulo-planeta">
          {{ planeta.name }}
      </div>
      <div class="informacoes-planeta">
          <div class="info-planeta"><span class="titulo-info">Population:</span> {{ planeta.population }}</div>
          <div class="info-planeta"><span class="titulo-info">Climate:</span> {{ planeta.climate}}</div>
          <div class="info-planeta"><span class="titulo-info">Terrain:</span> {{ planeta.terrain }}</div>
      </div>
      <div class="filmes-planeta" v-if="qtdFilms > 0">
          Featured in {{ qtdFilms }} film{{ qtdFilms>1?'s':'' }}
      </div>
  </div>
</template>

<script>
export default {
  name: 'Planeta',
  props:{
      planeta:{
        type:Object,
        required:true
      }
  },
  computed:{
      qtdFilms(){
          return this.planeta.films.length;
      }
  }
}
</script>

<style>
.planeta{
    min-width:400px;
    margin:auto;
    background-color:white;
    color: black;
    text-align: center;
    box-shadow: 0 3px 6px rgba(255,255,255,0.16), 0 3px 6px rgba(255,255,255,0.23);
}
.informacoes-planeta{
    padding:20px 20px;
}

.info-planeta{
    padding:10px;
}
.titulo-planeta{
    color:yellow;
    background-color: black;
    text-align: center;
    font-size: 2em;
    padding:10px;
    font-family: StarJediHollow,sans-serif;
}
.filmes-planeta{
    padding:10px;
}

</style>
