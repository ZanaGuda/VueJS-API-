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
            <CardItem v-for="news in newsList.results" :key="news.id" :cardTitle="news.name" :cardContent="news.overview" :cardImage="news.poster_path" :cardDate="news.first_air_date" :cardId="news.id">
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
            newsList: []
        }
    },
    methods: {
        fetchNews() {
            var url =
              'https://api.themoviedb.org/3/discover/movie?api_key=54106cb9e32f32a2f6c166158a3062d4&vote_average.gte=' + this.searchKeyRating + '&vote_average.lte=' + this.searchKeyRating + '&primary_release_year=' + this.searchKeyYear
            fetch(url)
                .then(response => response.json())
                .then(data => {
                    this.newsList = data;
                    console.log(this.newsList);
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
</style>
