<template>
  <main>
    <h2>AppMain</h2>
    <!-- Input e button per la ricerca da spostare poi nell Header -->
    <label>Ricerca qui il tuo film: </label>
    <input type="text" @keyup.enter="getMovies" v-model="inputText" id="search">
    <button @click="getMovies">Search</button>

    <div v-if="loading">Nessun Films ancora caricato...</div>
    <div v-else id="films">
        <!-- Card Film -->
        <div v-for="movie in moviesResults" :key="movie.id" class="film-card">
            <h3> {{movie.title}} </h3>
            <h4> {{movie.original_title}} </h4>
            <span><strong>Lingua: </strong> {{movie.original_language}}</span>
            <span><strong> Voto: </strong> {{movie.vote_average}}</span>
        </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios';

export default {
  name: 'AppMain',
  props: {
    
  },
  data() {
      return {
          apiKey: 'd1f8770b72ea44dd001003d5c3b3b323',
          apiUrl: 'https://api.themoviedb.org/3/search/',
          movies: [],
          loading: true,
          inputText: '',
          searchText: '',

      }
  },
  computed: {
      moviesResults(){
          return [...this.movies]
      }
  },
  methods: {
      getMovies(){
          this.searchText = this.inputText.toLowerCase();
          axios
          .get(this.apiUrl + 'movie',{
              params: {
                  api_key: this.apiKey,
                  query: this.searchText,
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
main{
    min-height: calc(100vh - 100px);
    background-color: #999;

}
</style>
