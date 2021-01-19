<template>
    <v-container>
        <v-row justify="space-around">
            <v-col cols="4">
                <button @click="toTheatres">In Theatres</button>
            </v-col>
            <v-col cols="4">
                <button  @click="toPopular">Popular</button>
            </v-col>
            <v-col cols="4">
                <button  @click="toTvShow">TV Shows</button>
            </v-col>
        </v-row>
        </div>
    </v-container>
</template>

<script>
export default {
    data () {
        return {
            navigasi : ''
        }
    },
    methods: {
        toTheatres () {
            this.navigasi = 'InTheatres'
        },
        toPopular () {
            this.navigasi = 'Popular'
        },
        toTvShow () {
            this.navigasi = 'TvShow'
        }
    }
}
</script>

<style>
#nav {
 display: flex;
 justify-content: center;
}

button {
    margin: 0px 30px;
    font-weight: bold;
    padding-bottom: 10px;
    border-bottom: 2px solid blue;
}
</style>