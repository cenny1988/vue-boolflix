<template>
  <main>
    <h2>AppMain</h2>
    <div v-if="loadOff">Nessun Films ancora caricato...</div>
    <div v-else id="lists">
        <h3>Lista Film</h3>
        <div class="lists">
            <CardMovie v-for="movie in moviesList" :key="movie.id" :detailsMovie="movie" class="film-card"/>
        </div>
        <h3>Lista Serie</h3>
        <div class="lists">
            <CardSerie v-for="serie in seriesList" :key="serie.id" :detailsSerie="serie" class="film-card"/>
        </div>
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

    .lists{
        display: flex;
        flex-wrap: wrap;
        margin: 1rem 0;

        .film-card{
            padding: .3rem;
            border: 1px solid #000;
        }
    }
}
</style>
