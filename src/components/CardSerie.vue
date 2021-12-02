<template>
  <section>
      <div class="film-card">
            <h3> {{detailsSerie.name}} </h3>
            <h4> {{detailsSerie.original_name}} </h4>
            <country-flag v-if="detailsSerie.original_language === 'en' " :country="'gb-eng'" size='normal'/>
            <country-flag v-else :country="detailsSerie.original_language" size='normal'/>
            <!-- {{detailsSerie.original_language}} -->
            <!-- <span><strong>Lingua: </strong> {{detailsSerie.original_language}}</span> -->
            <span><strong> Voto: </strong> {{detailsSerie.vote_average}}</span>
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
  computed:{
    //   flags(){
    //     //   if (this.detailsSerie.original_language === 'en' ){
    //     //       return this.detailsSerie.original_language = 'gb-eng';
    //     //   }
    //       return this.detailsSerie.original_language === 'en' ? this.detailsSerie.original_language = 'gb-eng' : this.detailsSerie.original_language
    //   }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    
</style>