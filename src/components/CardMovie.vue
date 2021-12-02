<template>
  <section>
      <div class="film-card">
            <img v-if="detailsMovie.poster_path !== null" :src="imageUrl + posterSize + detailsMovie.poster_path" :alt="detailsMovie.name">
            <img v-else src="../assets/img/img-not-found.png" :alt="detailsMovie.name">
            <h3> {{detailsMovie.title}} </h3>
            <h4> {{detailsMovie.original_title}} </h4>
            <!-- serie di v-if per controllo flags -->
            <country-flag v-if="detailsMovie.original_language === 'en' " :country="'gb-eng'" size='normal'/>
            <country-flag v-else-if="detailsMovie.original_language === 'zh' || detailsMovie.original_language === 'hi' " :country="'cn'" size='normal'/>
            <country-flag v-else-if="detailsMovie.original_language === 'ja' " :country="'jp'" size='normal'/>
            <country-flag v-else :country="detailsMovie.original_language" size='normal'/>
            <!-- {{detailsMovie.original_language}} -->

            <span><strong> Voto: </strong> {{detailsMovie.vote_average}}</span>
            <font-awesome-icon icon="star" />

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
      }
  },
  computed: {
    // potrei prendere detailsMovie.original_language e verificare qui l esistenza della flag...
  },
  methods: {
    
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>