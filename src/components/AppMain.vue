<template>
  <main>
    <h2>AppMain</h2>
    <div v-if="loadOff">Nessun Films ancora caricato...</div>
    <div v-else id="films">
        <div v-for="movie in moviesList" :key="movie.id" class="film-card">
            <h3> {{movie.title}} </h3>
            <h4> {{movie.original_title}} </h4>
            <span><strong>Lingua: </strong> {{movie.original_language}}</span>
            <span><strong> Voto: </strong> {{movie.vote_average}}</span>
        </div>
    </div>
  </main>
</template>

<script>

export default {
  name: 'AppMain',
  props: {
      moviesList: Array,
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
