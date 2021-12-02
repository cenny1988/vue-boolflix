<template>
  <section>
      <div class="film-card">
            <h3> {{detailsMovie.title}} </h3>
            <h4> {{detailsMovie.original_title}} </h4>
            <country-flag v-if="detailsMovie.original_language === 'en' " :country="'gb-eng'" size='normal'/>
            <country-flag v-else-if="detailsMovie.original_language === 'zh' || detailsMovie.original_language === 'hi' " :country="'cn'" size='normal'/>
            <country-flag v-else-if="detailsMovie.original_language === 'ja' " :country="'jp'" size='normal'/>
            <country-flag v-else :country="detailsMovie.original_language" size='normal'/>
            {{detailsMovie.original_language}}
            <!-- <span><strong>Lingua: </strong> {{detailsMovie.original_language}}</span> -->
            <span><strong> Voto: </strong> {{detailsMovie.vote_average}}</span>
      </div>
  </section>
</template>

<script>
import CountryFlag from 'vue-country-flag';

export default {
  name: 'CardMovie',
  components: {
    CountryFlag,
  },
  props: {
    detailsMovie: Object,
  },
  computed: {
    // potrei prendere detailsMovie.original_language e verificare qui l esistenza della flag...
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>