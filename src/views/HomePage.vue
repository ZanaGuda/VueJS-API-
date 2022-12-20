<template>
<div id="app">
    <div class="container">
        <div class="search">
            <input type="text" v-model="input">
            <br>
            <input type="text" v-model="rate">
            <button type="button" class="btn btn-primary" style="margin-left:10px" @click="fetchNews()">Search</button>
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
            input: "",
            rate: "",
            newsList: []
        }
    },
    methods: {
        fetchNews() {
            var url =
              'https://api.themoviedb.org/3/discover/movie?api_key=54106cb9e32f32a2f6c166158a3062d4&vote_average.gte=' + this.rate + '&vote_average.lte=' + this.rate + '&primary_release_year=' + this.input
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
