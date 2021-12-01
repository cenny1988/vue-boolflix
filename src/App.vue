<template>
  <div id="app">
    <AppHeader @searchUser="getMovies"/>
    <!-- <div v-if="loading">Nessun Films ancora caricato...</div>
    <div v-else id="films">
        <div v-for="movie in moviesResults" :key="movie.id" class="film-card">
            <h3> {{movie.title}} </h3>
            <h4> {{movie.original_title}} </h4>
            <span><strong>Lingua: </strong> {{movie.original_language}}</span>
            <span><strong> Voto: </strong> {{movie.vote_average}}</span>
        </div>
    </div> -->
    <AppMain
      :moviesList="movies"
      :loadingStop="loading"
    />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    AppHeader,
    AppMain
  },
  data() {
    return {
      apiKey: 'd1f8770b72ea44dd001003d5c3b3b323',
      apiUrl: 'https://api.themoviedb.org/3/search/',
      movies: [],
      loading: true,
    }
  },
  computed: {
      moviesResults(){
          // this.getMovies();
          return [...this.movies]
      }
  },  
  methods: {
    getMovies(valueSearch){
          axios
          .get(this.apiUrl + 'movie',{
              params: {
                  api_key: this.apiKey,
                  query: valueSearch,
                  language: 'it-IT'
              }
          })
          .then((res) => {
              this.movies = res.data.results;
              this.loading = false;
          })
          .catch((err) => {
              console.log("Errore: ", err);
          });
      },
  },
}
</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: sans-serif;
  background-color: #555;
}
</style>
