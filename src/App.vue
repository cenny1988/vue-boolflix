<template>
  <div id="app">
    <AppHeader @searchUser="research"/>
    
    <AppMain
      :moviesList="moviesResults"
      :seriesList="seriesResults"
      :loadingStop="loading"
      :genresList="genres"
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
      genres: [],
      loading: true,
      find: false,
    }
  },
  created() {
    this.getGenres();
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
    // chiamata axios x lista generi movie
    getGenres(){
          axios
          .get('https://api.themoviedb.org/3/genre/movie/list',{
              params: {
                  api_key: this.apiKey,
                  language: 'it'
              }
          })
          .then((res) => {
            this.genres = res.data.genres;
          })
          .catch((err) => {
              console.log("Errore: ", err);
          });
    // ciamata axios x lista generi serie tv
          axios
          .get('https://api.themoviedb.org/3/genre/tv/list',{
              params: {
                  api_key: this.apiKey,
                  language: 'it'
              }
          })
          .then((res) => {
            // creamo un unico array con la somma della lista generi dei 2 risultati (film+serie) 
            // this.genres = [...this.genres, ...res.data.genres]; ---> non verifica i doppioni
            res.data.genres.forEach(element => {
              this.genres.forEach(el => {
                if (element.id === el.id) {
                  this.find = true;
                }
              });
              if (this.find === false){
                this.genres.push(element);
              }else this.find = false;
            });
          })
          .catch((err) => {
              console.log("Errore: ", err);
          });
      },
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
