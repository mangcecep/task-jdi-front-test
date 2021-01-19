<template>
        <div v-if="movies.length">
          <VueSlickCarousel v-bind="slickOptions">
            <div class="carousel-wrapper" v-for="(movie, index) in movies" :key="index">
              <router-link :to="{ name: 'detail', params: { id: movie.id , keys : api_key}}">
                <div class="img-wrapper">
                    <img :src="`https://image.tmdb.org/t/p/original${ movie.poster_path }`" alt="carousel" />
                </div>
                <p><b>{{ movie.title }} </b></p>
              </router-link>
              <p>
                <v-icon slot="append" color="yellow"> 
                  mdi-star
                </v-icon> <span> {{ movie.vote_average }} </span>
              </p>
            </div>
          </VueSlickCarousel>
        </div>
        <div v-else-if="error">
          <p>{{ err.message }} </p>
        </div>
        <div v-else>
          <p> loading movies ... </p>
        </div>
</template>

<script>
  export default {
    props: ["navigasi"],
    data () {
        return {
          slickOptions: {
            slidesToShow: 1,
            slidesToScroll: 1,
            swipeToSlide: true,
            arrows: false,
            infinite: true,
            centerMode: true,
            responsive: [
              {
                breakpoint: 1024,
                slickOptions: {
                  slidesToShow: 3,
                  slidesToScroll: 3,
                  infinite: true,
                  dots: true
                }
              },
              {
                breakpoint: 600,
                slickOptions: {
                  slidesToShow: 2,
                  slidesToScroll: 2,
                  initialSlide: 2
                }
              },
              {
                breakpoint: 420,
                slickOptions: {
                  slidesToShow: 1,
                  slidesToScroll: 1,
                  centerMode: true,
                }
              }
            ]
          },
          movies: [],
          error: null,
          sortBy: 'popularity',
          api_key: 'e2f3842d3dc69632ce5239805027600e'
        }
    },
    mounted () {
    fetch(`https://api.themoviedb.org/3/discover/movie?sort_by=${this.sortBy}.desc&api_key=${this.api_key}`)
      .then(res => res.json())
        .then(data => {
            this.movies = data.results
        })
        .catch(err => {
            this.error = console.log(err)
        })
    }
  }
</script>

<style scoped>
.carousel-wrapper {
  padding: 10px;
}
.img-wrapper img {
  margin: auto;
  width: 400px;
  height: auto;
  border-radius: 30px 30px;
}
@media print, screen and (max-width: 420px) {
  .img-wrapper img {
    width: 250px;
    height: auto;
  }
}
@media print, screen and (max-width: 360px) {
  .img-wrapper img {
    width: 200px;
    height: auto;
  }
}
p {
    text-align: center;
    color: black;
}
a:link {
  text-decoration: none;
}

</style>