<template>
  <main>
    <h2>AppMain</h2>
    <div v-if="loading">Nessun Films ancora caricato...</div>
    <div v-else id="films">
        <div v-for="film, index in films" :key="index" class="film-card">
            <h3> {{film.title}} </h3>
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
          apiUrl: "https://api.themoviedb.org/3/search/movie?api_key=d1f8770b72ea44dd001003d5c3b3b323&query=ritorno+al+futuro",
          films: [],
          loading: true,

      }
  },
  created() {
      this.getFilms();
  },
  methods: {
      getFilms(){
          axios
          .get(this.apiUrl)
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
