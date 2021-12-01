<template>
  <main>
    <h2>AppMain</h2>
    <!-- Input e button per la ricerca da spostare poi nell Header -->
    <label>Ricerca qui il tuuo film: </label>
    <input type="text" @keyup.enter="getFilms" v-model="inputText" id="search">
    <button @click="getFilms">Search</button>

    <div v-if="loading">Nessun Films ancora caricato...</div>
    <div v-else id="films">
        <!-- Card Film -->
        <div v-for="film in films" :key="film.id" class="film-card">
            <h3> {{film.title}} </h3>
            <h4> {{film.original_title}} </h4>
            <span><strong>Lingua: </strong> {{film.original_language}}</span>
            <span><strong> Voto: </strong> {{film.vote_average}}</span>
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
          films: [],
          loading: true,
          inputText: '',
          searchText: '',

      }
  },
  created() {
  },
  computed: {
  },
  methods: {
      getFilms(){
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
              this.films = res.data.results;
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
