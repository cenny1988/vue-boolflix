<template>
  <main>
    <h2>AppMain</h2>
    <div v-if="loadOff">Nessun Films ancora caricato...</div>
    <div v-else id="films">
        <h3>Lista Film</h3>
        <div v-for="movie in moviesList" :key="movie.id" class="film-card">
            <h3> {{movie.title}} </h3>
            <h4> {{movie.original_title}} </h4>
            <span><strong>Lingua: </strong> {{movie.original_language}}</span>
            <span><strong> Voto: </strong> {{movie.vote_average}}</span>
        </div>
        <br>
        <h3>Lista Serie</h3>
        <div v-for="serie in seriesList" :key="serie.id" class="film-card">
            <h3> {{serie.name}} </h3>
            <h4> {{serie.original_name}} </h4>
            <span><strong>Lingua: </strong> {{serie.original_language}}</span>
            <span><strong> Voto: </strong> {{serie.vote_average}}</span>
        </div>
    </div>
  </main>
</template>

<script>

export default {
  name: 'AppMain',
  props: {
      moviesList: Array,
      seriesList: Array,
      loadOff: Boolean,
  },
  data() {
      return {
        // loading: true,
      }
  },
  methods: {

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
main{
    min-height: calc(100vh - 100px);
    background-color: #999;

}
</style>
