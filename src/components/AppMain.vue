<template>
  <main>
    
    <div v-if="loadOff">Nessun Films ancora caricato...</div>
    <div v-else id="list-card">
        <!-- <h3>Lista Film</h3> -->
        <div class="lists">
            <CardMovie v-for="movie in moviesList" :key="movie.id" :detailsMovie="movie" class="film-card"/>
        </div>
        <!-- <h3>Lista Serie</h3> -->
        <div class="lists">
            <CardSerie v-for="serie in seriesList" :key="serie.id" :detailsSerie="serie" class="film-card"/>
        </div>
    </div>

  </main>
</template>

<script>
import CardMovie from '@/components/CardMovie.vue';
import CardSerie from '@/components/CardSerie.vue';

export default {
  name: 'AppMain',
  components: {
      CardMovie,
      CardSerie,
  },
  props: {
      moviesList: Array,
      seriesList: Array,
      loadOff: Boolean,
  },
  data() {
      return {
        // loading: true,
      }
  },
  methods: {
      
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
main{
    min-height: calc(100vh - 100px);
    background-color: #434343;
    

    .lists{
        display: flex;
        flex-wrap: wrap;
        

        .film-card{
            flex-basis: calc(100% / 5 - 2px);
            margin: 0 1px .5rem;
            cursor: pointer;
            position: relative;
            height: 570px;
            

            &:hover{
                .detail-card{
                    display: block;
                }
            }

            img{
                width: 100%;
                height: 100%;
                object-fit: cover;
                // border-radius: 20px;
            
            }

            .detail-card{
                display: none;
                position: absolute;
                top: 0;
                left: 0;
                right: 0;
                bottom: 0;
                background-color: #434343;
                padding: 2rem .4rem;

                h3, h4, div{
                    margin-bottom: .7rem;
                }
                h3{
                    font-size: 2rem;
                }
                .vote{
                    text-align: center;
                }
                div{
                    span{
                        margin-right: 10px;
                    }
                }
                
            }

        }
    }
}
</style>
