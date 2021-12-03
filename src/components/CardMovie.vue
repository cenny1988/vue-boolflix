<template>
  <section>
      <div class="film-card">
        <!-- img card -->
        <img v-if="detailsMovie.poster_path !== null" :src="imageUrl + posterSize + detailsMovie.poster_path" :alt="detailsMovie.name">
        <img v-else src="../assets/img/img-not-found.png" :alt="detailsMovie.name">

        <!-- titolo -->
        <h3> {{detailsMovie.title}} </h3>
        <!-- titolo originale -->
        <h4> {{detailsMovie.original_title}} </h4>

        <!-- serie di v-if per controllo flags -->
        <country-flag :country="setFlag(detailsMovie)" size='normal'/>

        <!-- voto con star -->
        <span><strong> Voto: </strong> {{setVote(detailsMovie)}}</span>
        <span><font-awesome-icon v-for="n, index in vote" :key="index" icon="star" /></span>

      </div>
  </section>
</template>

<script>
import CountryFlag from 'vue-country-flag';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faStar } from '@fortawesome/free-solid-svg-icons';

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
      }
  },
  computed: {
    // potrei prendere detailsMovie.original_language e verificare qui l esistenza della flag...
  },
  methods: {
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

</style>