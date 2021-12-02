<template>
  <main>
    <h2>AppMain</h2>
    <div v-if="loadOff">Nessun Films ancora caricato...</div>
    <div v-else id="films">
        <h3>Lista Film</h3>
        <CardMovie v-for="movie in moviesList" :key="movie.id" :detailsMovie="movie" class="film-card"/>
        <br>
        <h3>Lista Serie</h3>
        <CardSerie v-for="serie in seriesList" :key="serie.id" :detailsSerie="serie" class="film-card"/>
    </div>
  </main>
</template>

<script>
import CardMovie from '@/components/CardMovie.vue';
import CardSerie from '@/components/CardSerie.vue';

export default {
  name: 'AppMain',
  components: {
      CardMovie,
      CardSerie,
  },
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
