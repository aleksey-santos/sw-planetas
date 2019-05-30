<template>
  <div class="planeta">
      <div class="titulo-planeta">
          {{ planeta.name }}
      </div>
      <div class="informacoes-planeta">
          <div class="info-planeta">Population: {{ planeta.population }}</div>
          <div class="info-planeta">Climate: {{ planeta.climate}}</div>
          <div class="info-planeta">Terrain: {{ planeta.terrain }}</div>
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

</style>
