<template>
  <div class="container">
  <article class="single-article">
    <div class="container">
      <div class="single-article__title">
        <div>{{ articleTitle }}</div>
      </div>
      <div class="single-article__image">
        <img :src="'https://image.tmdb.org/t/p/w500/' + articleImage" alt="">
      </div>
      <div class="single-article__content content">
        <div >{{ articleContent }} </div>
      </div>
      <div class="single-article__rating" style="color:white">
        <div>Rating: {{ articleRating }}</div>
      </div>
    </div>
  </article> 
  <p style="display: flex;
    justify-content: center;
    align-items: center;
    font-size: 50px;
    font-weight: 900; color: white;">SIMILAR MOVIES</p>
  <div class="card-list">
   
  <CardItem v-for="news in similarMovies.results" :key="news.id" :cardTitle="news.name" :cardContent="news.overview"
    :cardImage="news.poster_path" :cardDate="news.first_air_date" :cardId="news.id">
  </CardItem>

</div></div>
</template>

<script>
import CardItem from "../components/CardItem.vue"
export default {
  name: 'SingleMovie',
  components: {
    CardItem
  },
  data() {
    return {
      articleContent: '',
      articleImage: '',
      articleTitle: '',
      articleRating: '',
      similarMovies: []
    }
  },
  methods: {
    fetchSingleNews(newsID) {
      fetch('https://api.themoviedb.org/3/movie/' + newsID + "?api_key=c246ec55d79f150e771a55ba99fa6c78")
      .then(response => response.json())
      .then(data => {
        console.log(data);
        this.articleTitle = data.title;
        this.articleContent = data.overview;
        this.articleImage = data.poster_path;
        this.articleRating = data.vote_average;
        
      })
    },
    fetchSimiliarMovies(newsID) {
      fetch("https://api.themoviedb.org/3/movie/" + newsID + "/similar?api_key=c246ec55d79f150e771a55ba99fa6c78&language=en-US")
        .then(response => response.json())
        .then(data => {
          this.similarMovies = data
        });
    },
  },
  mounted() {
    this.fetchSingleNews(this.$route.params.id);
    this.fetchSimiliarMovies(this.$route.params.id);
  }
}
</script>

<style>
.single-article__content{
  color: white;
}
.single-article {
  padding-top: 60px;
  padding-bottom: 60px;
  text-align: left;
  
}
.single-article__title{
      font-size: 50px;
        font-weight: 500;
        display: flex;
        justify-content: center;
        color: white;
}
.single-article__image{
      display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 10px;
}
</style>