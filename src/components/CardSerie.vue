<template>
      <section class="col p-0 m-0 film-card">
            <!-- img card -->
            <img class="card-img-top" v-if="detailsSerie.poster_path !== null" :src="imageUrl + posterSize + detailsSerie.poster_path" :alt="detailsSerie.name">
            <img class="card-img-top" v-else src="../assets/img/netflix-card.png" :alt="detailsSerie.name">

            <div class="detail-card card-body bg-dark text-white text-center ">
                <!-- titolo -->
                <h3> {{detailsSerie.name}} </h3>
                <!-- titolo originale -->
                <h4> {{detailsSerie.original_name}} </h4>

                <div>
                    <span><country-flag :country="setFlag(detailsSerie)" size='normal'/></span>
                    <!-- voto con star -->
                    <span><strong> Voto: </strong> {{setVote(detailsSerie)}}</span>
                    <span class="star"><font-awesome-icon v-for="n, index in vote" :key="index" icon="star" /></span>
                </div>

                <a @click="getCast(detailsSerie.id)" class="btn btn-primary ">SHOW CAST</a>
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
  name: 'CardSerie',
  components: {
    CountryFlag,
  },
  props: {
    detailsSerie: Object,
  },
  data() {
      return {
          imageUrl: 'https://image.tmdb.org/t/p/',
          posterSize: 'w342',
          vote: null,
          lang: '',
          apiKey: 'd1f8770b72ea44dd001003d5c3b3b323',
          apiUrl: 'https://api.themoviedb.org/3/',
          casts: [],
      }
  },
  computed:{
      castResults(){
          return [...this.casts.slice(0, 5)]
      },
      },
  methods: {
      getCast(index){
          axios
          .get(this.apiUrl + 'tv/' + index + '/credits',{
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