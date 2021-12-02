<template>
  <section>
      <div class="film-card">
            <h3> {{detailsMovie.title}} </h3>
            <h4> {{detailsMovie.original_title}} </h4>
            <span><strong>Lingua: </strong> {{detailsMovie.original_language}}</span>
            <span><strong> Voto: </strong> {{detailsMovie.vote_average}}</span>
      </div>
  </section>
</template>

<script>
export default {
  name: 'CardMovie',
  props: {
    detailsMovie: Object,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>