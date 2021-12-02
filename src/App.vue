<template>
  <div id="app">
    <AppHeader @searchUser="research"/>
    
    <AppMain
      :moviesList="movies"
      :seriesList="series"
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
      series: [],
      all: [],
      loading: true,
    }
  },
  computed: {
      moviesResults(){
          return [...this.movies];
      },
      seriesResults(){
          return [...this.series];
      },
  },  
  methods: {
    getMovies(value, type){
          axios
          .get(this.apiUrl + type,{
              params: {
                  api_key: this.apiKey,
                  query: value,
                  language: 'it'
              }
          })
          .then((res) => {
              this.movies = res.data.results;
          })
          .catch((err) => {
              console.log("Errore: ", err);
          });
          // console.log(this.movies);
      },
    getSeries(value, type){
          axios
          .get(this.apiUrl + type,{
              params: {
                  api_key: this.apiKey,
                  query: value,
                  language: 'it'
              }
          })
          .then((res) => {
              this.series = res.data.results;
          })
          .catch((err) => {
              console.log("Errore: ", err);
          });
          // console.log(this.series);
      },
    research(valueSearch){
          this.getMovies(valueSearch, 'movie');
          this.getSeries(valueSearch, 'tv');
          this.loading = false;
          
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
