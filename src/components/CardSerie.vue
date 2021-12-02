<template>
  <section>
      <div class="film-card">
            <h3> {{detailsSerie.name}} </h3>
            <h4> {{detailsSerie.original_name}} </h4>
            <span><strong>Lingua: </strong> {{detailsSerie.original_language}}</span>
            <span><strong> Voto: </strong> {{detailsSerie.vote_average}}</span>
      </div>
  </section>
</template>

<script>
export default {
  name: 'CardSerie',
  props: {
    detailsSerie: Object,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>