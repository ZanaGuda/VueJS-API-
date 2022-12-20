<template>
<div id="app">
    <div class="container">
        <div class="search">
          <label class="label">Year based Search</label>
            <input type="text" v-model="searchKeyYear">
            <br>
            <label class="label">Rating based Search</label>
            <input type="text" v-model="searchKeyRating">
            <button type="button" class="btn btn-primary" style="margin-left:10px" v-on:click="fetchNews()">Search</button>
        </div>
        <div class="card-list">
            <CardItem v-for="movies in movieList.results" :key="movies.id" :cardTitle="movies.name" :cardContent="movies.overview" :cardImage="movies.poster_path" :cardDate="movies.first_air_date" :cardId="movies.id">
            </CardItem>
        </div>
    </div>
</div>
</template>

<script>
import CardItem from '../components/CardItem.vue';

export default {
    name: 'HomePage',
    components: {
        CardItem,

    },
    data() {
        return {
            searchKeyYear: "",
            searchKeyRating: "",
            movieList: []
        }
    },
    methods: {
        fetchNews() {
            var url =
              'https://api.themoviedb.org/3/discover/movie?api_key=c246ec55d79f150e771a55ba99fa6c78&vote_average.gte=' + this.searchKeyRating + '&vote_average.lte=' + this.searchKeyRating + '&primary_release_year=' + this.searchKeyYear 
            fetch(url)
                .then(response => response.json())
                .then(data => {
                    this.movieList = data;
                    console.log(this.movieList);
                })
        }
    },
    mounted() {
        this.fetchNews();
    }
}

</script>

<style>
.card-list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
    padding-top: 60px;
    padding-bottom: 60px;
}

img {
    object-fit: cover !important;
}
.btn.btn-primary{
    margin-left: 0px !important;
    margin-top: 20px;
    /* margin-top: -75px; */
    display: flex;
}
@media(max-width:767px){
 .card-list{
  display: grid;
  grid-template-columns: 1fr;
 }

}
</style>
