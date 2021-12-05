<template>
  <section class="col p-0 m-0 film-card">
        <!-- img card -->
        <img class="card-img-top" v-if="detailsMovie.poster_path !== null" :src="imageUrl + posterSize + detailsMovie.poster_path" :alt="detailsMovie.name">
        <img class="card-img-top" v-else src="../assets/img/netflix-card.png" :alt="detailsMovie.name">

        <div class="detail-card card-body bg-dark text-white text-center ">
          <!-- titolo -->
          <h3 class="card-title">{{detailsMovie.title}} </h3>
          <!-- titolo originale -->
          <h4>{{detailsMovie.original_title}} </h4>

          <div>
            <span><country-flag :country="setFlag(detailsMovie)" size='normal'/></span>
            <!-- voto con star -->
            <span><strong> Voto: </strong> {{setVote(detailsMovie)}}</span>
            <span class="star"><font-awesome-icon v-for="n, index in vote" :key="index" icon="star" /></span>
          </div>

          <a @click="getCast(detailsMovie.id)" class="btn btn-primary ">SHOW CAST</a>
          <div class="card-text">
            <div v-for="cast,i in castResults" :key="i">{{cast.name}}</div>
          </div>
        </div>
  </section>
</template>

<script>
import CountryFlag from 'vue-country-flag';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faStar } from '@fortawesome/free-solid-svg-icons';
import axios from 'axios';

library.add(faStar);

export default {
  name: 'CardMovie',
  components: {
    CountryFlag,
  },
  props: {
    detailsMovie: Object,
  },
  data() {
      return {
          imageUrl: 'https://image.tmdb.org/t/p/',
          posterSize: 'w342',
          vote: null,
          apiKey: 'd1f8770b72ea44dd001003d5c3b3b323',
          apiUrl: 'https://api.themoviedb.org/3/',
          casts: [],
      }
  },
  computed: {
    castResults(){
          return [...this.casts.slice(0, 5)]
      },
  },
  methods: {
    getCast(index){
          axios
          .get(this.apiUrl + 'movie/' + index + '/credits',{
              params: {
                  api_key: this.apiKey,
                  language: 'it'
              }
          })
          .then((res) => {
              this.casts = res.data.cast;
          })
          .catch((err) => {
              console.log("Errore: ", err);
          });
          // console.log(this.casts);
    },
    setVote(card){
        this.vote = Math.round(card.vote_average/2);
    },
    setFlag(card){
        if (card.original_language === 'en') {
            this.lang = 'gb-eng';
        }
        else if (card.original_language === 'zh' || card.original_language === 'hi') {
            this.lang = 'cn';
        }
        else if (card.original_language === 'ja') {
            this.lang = 'jp';
        }
        else this.lang = card.original_language;
        return this.lang
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.star{
  color: gold;
}

</style>