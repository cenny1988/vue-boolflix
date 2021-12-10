<template>
  <main>
    <!-- Differentemente dall Header per il Main e le card utilizzato Bootstrap Vanilla -->
    <div class="container-lg" v-if="loadOff">Nessun Films ancora caricato...</div>
    <div class="" v-else id="list-card" >
        <div class="container-fluid">
            <div class="row row-cols-1 row-cols-sm-2  row-cols-md-4 row-cols-lg-6">
                <CardMovie v-for="movie in moviesList" :key="movie.id" :detailsMovie="movie" :genLists="genresList"/>
                <CardSerie v-for="serie in seriesList" :key="serie.id" :detailsSerie="serie" :genLists="genresList"/>
            </div>
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
      genresList: Array,
  },
  data() {
      return {
        genres: [],
      }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
main{
    section{
        padding: 0;
    }
    min-height: calc(100vh - 100px);
    background-color: #434343;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;

    .film-card{
        cursor: pointer;
        position: relative;
            

        &:hover{
            .detail-card{
                display: block;
            }
        }

        .card-img, .card-img-top {
            border-top-left-radius: none;
            border-top-right-radius: none;
            
            min-height: 600px;
            object-fit: fill;
                
        }

        .detail-card{
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            padding-top: 4rem;
        }
    }
}
</style>
