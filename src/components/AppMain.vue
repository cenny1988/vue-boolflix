<template>
  <main>
    <!-- Differentemente dall Header per il Main e le card utilizzato Bootstrap Vanilla -->
    <!-- iframe con traile in primo piano -->
    <div class="trailer">
        <section>
            <iframe width="560" height="315" src="https://www.youtube.com/embed/2cOzXxfuwqM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
            <div class="dettagli-video">
                <img src="https://occ-0-2908-2774.1.nflxso.net/dnm/api/v6/tx1O544a9T7n8Z_G12qaboulQQE/AAAABbDPbGOaZ2jDzuKx0Qqz4AkcP6LopQGYezdUkfKGMXLtiOIiVdNvxH1oPi0GyWjpti0wySwGT6wQSTXe4mA04YwzGeI-vEZjBaFRG2ipM0EWZ7XI8ZyvpUfT2JnX4tYlpdgxkxZEfaLue_N3_Xlj9lDUWGtP4QuQW7os9jyaC7b5.webp?r=695" alt="">
                <div class="trama">In 1990s Berlin, an artist and a hacker invented a new way to see the world. Years later, they reunite to sue Google for patent infringement on it.</div>
                <button class="play"><i class="fas fa-play"></i> Play</button>
                <button class="info"><span class="circle">i</span> <span>More Info</span></button>
            </div>
        </section>
    </div>
    <!-- main -->
    <div class="container-lg" v-if="loadOff">Nessun Films ancora caricato...</div>
    <div class="" v-else id="list-card" >
        <div class="container-fluid">
            <div class="row row-cols-1 row-cols-sm-2  row-cols-md-4 row-cols-lg-5">
                <CardMovie v-for="movie in moviesList" :key="movie.id" :detailsMovie="movie" :genLists="genresList"/>
                <CardSerie v-for="serie in seriesList" :key="serie.id" :detailsSerie="serie" :genLists="genresList"/>
            </div>
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
      genresList: Array,
  },
  data() {
      return {
        genres: [],
      }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
main{
// sezone video trailer
    .trailer{
        section{
            position: relative;
            iframe{
                width: 100%;
                height: 700px;
            }
            .dettagli-video{
                position: absolute;
                left: 100px;
                bottom: 150px;
                width: 600px;
                .trama{
                    color: white;
                    font-size: 20px;
                    font-family: 'Poppins', sans-serif;
                    padding-top: 10px;
                }
                .play{
                    background-color: white;
                    border-radius: 5px;
                    padding: 12px 27px;
                    border: none;
                    color: black;
                    font-size: 18px;
                    font-weight: bold;
                    margin: 20px 10px 0 0;
                    cursor: pointer;
                    i{
                        padding-right: 5px;
                    }
                }
                .info{
                    background-color: #7c7b7b;
                    opacity: 0.8;
                    border-radius: 5px;
                    padding: 12px 27px;
                    border: none;
                    color: white;
                    font-size: 18px;
                    font-weight: bold;
                    cursor: pointer;
                    .circle{
                        padding: 0 7px;
                        border: 3px solid white;
                        border-radius: 50%;
                        margin-right: 8px;
                    }
                }
            }
            .dettagli-video .play:hover{
                opacity: 0.7;
            }
            .dettagli-video .info:hover{
                opacity: 0.6;
            }
        }
    }
    // sezione main con cards
    section{
        padding: 0;
    }
    min-height: calc(100vh - 100px);
    background-color: #434343;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;

    .film-card{
        cursor: pointer;
        position: relative;
        overflow: auto;
            

        &:hover{
            .detail-card{
                display: block;
            }
        }

        .card-img, .card-img-top {
            border-top-left-radius: none;
            border-top-right-radius: none;
            
            min-height: 600px;
            object-fit: fill;
                
        }

        .detail-card{
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            padding-top: 1rem;
        }
    }
}
</style>
