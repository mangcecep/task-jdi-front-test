<template>
    <div v-if="movie">
        <v-container>
            <img :src="`https://image.tmdb.org/t/p/original${ movie.backdrop_path }`" alt="poster"/>
            <v-card-subtitle>
                <div class="header">
                    <v-row>
                        <v-col cols="4">
                            <center>
                                <v-icon slot="append" color="yellow" class="head"> 
                                mdi-star
                                </v-icon> <br><span> {{ movie.vote_average }} / 10</span>
                                <br><span> {{ movie.vote_count }}</span>
                            </center>
                        </v-col>
                        <v-col cols="4">
                            <center>
                                <v-icon slot="append" color="black" class="head"> 
                                mdi-star-outline
                                </v-icon> <br><span> Rate This </span>
                            </center>
                        </v-col>
                        <v-col cols="4">
                            <center>
                                <span class="head meta">86</span><br><br>
                                <span class="subhead">Metascore</span><br>
                                <span>62 critic reviews</span>
                            </center>
                        </v-col>
                    </v-row>
                </div>
            </v-card-subtitle>
            <v-card>
                <h2>{{ movie.original_title }}</h2>
                <v-row>
                    <v-col cols="4">
                        <p class="ml-4 mt-4">{{ movie.release_date }}</p>
                    </v-col>
                    <v-col cols="4">
                        <p class="ml-4 mt-4">PG -13</p>
                    </v-col>
                    <v-col cols="4">
                        <p class="ml-4 mt-4">2h 32min</p>
                     </v-col>
                    <v-col cols="12">
                       <h3>Tagline : {{movie.tagline}}</h3>
                    </v-col>
                    <v-col cols="12">
                        <p>{{ movie.overview }}</p>
                    </v-col>
                </v-row>
            </v-card>
        </v-container>
    </div>
    <div v-else>
        <p>Loading ... </p>
    </div>
</template>

<script>
export default {
 async asyncData({ params, $axios }) {
     const movie = await $axios.$get(`https://api.themoviedb.org/3/movie/${params.id}?&api_key=${params.keys}`)
     return { movie }
 },
}
</script>

<style>
img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  border-radius: 30px 30px;
}
.head {
    margin-bottom: 10px;
}
.header {
    background: rgb(223, 222, 222);
    padding : 20px 20px;
    border-radius: 30px 0px 0px 30px;
    position: absolute;
    width: 400px;
    height: auto;
    margin-left: 129px;
    margin-top: -144px;
} 
.meta {
    background: rgb(4, 247, 105);
    padding: 10px 10px;
    color: azure;
}
center {
    font-size: 12px;
}
@media print, screen and (max-width: 420px) {
  img {
   width: 380px;
    height: auto;
  }
  .header {
    font-size: 1px;
    background: rgb(223, 222, 222);
    padding : 20px 20px;
    border-radius: 30px 0px 0px 30px;
    position: relative;
    width: 350px;
    height: auto;
    margin-left: 15px;
    margin-top: -100px;
  }
}
@media print, screen and (max-width: 360px) {
  img {
    width: 300px;
    height: auto;
  }
  .header {
    font-size: 1px;
    background: rgb(223, 222, 222);
    padding : 20px 20px;
    border-radius: 30px 0px 0px 30px;
    position: relative;
    width: 280px;
    height: auto;
    margin-left: 10px;
    margin-top: -100px;
} 
}
</style>