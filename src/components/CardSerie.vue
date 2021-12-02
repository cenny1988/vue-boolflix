<template>
  <section>
      <div class="film-card">
            <img v-if="detailsSerie.poster_path !== null" :src="imageUrl + posterSize + detailsSerie.poster_path" :alt="detailsSerie.name">
            <img v-else src="../assets/img/img-not-found.png" :alt="detailsSerie.name">
            <h3> {{detailsSerie.name}} </h3>
            <h4> {{detailsSerie.original_name}} </h4>
            <country-flag v-if="detailsSerie.original_language === 'en' " :country="'gb-eng'" size='normal'/>
            <country-flag v-else-if="detailsSerie.original_language === 'zh' || detailsSerie.original_language === 'hi' " :country="'cn'" size='normal'/>
            <country-flag v-else-if="detailsSerie.original_language === 'ja' " :country="'jp'" size='normal'/>
            <country-flag v-else :country="detailsSerie.original_language" size='normal'/>
            <!-- {{detailsSerie.original_language}} -->
           
            <!-- <span><strong> Voto: </strong> {{detailsSerie.vote_average}}</span> -->
            <span><strong> Voto: </strong> {{setVote(detailsSerie)}}</span>
      </div>
  </section>
</template>

<script>
import CountryFlag from 'vue-country-flag';

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
      }
  },
  computed:{
      },
  methods: {
      setVote(card){
        this.vote = card.vote_average;
        console.log(this.vote);
        return(this.vote);
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    
</style>